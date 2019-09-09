# The anko module

As introduced in [the search modules documentation](#!search/searchmodules.md#Anko), Gravwell's anko module is a general-purpose scripting tool within the search pipeline. It allows extremely flexible manipulations of search entries, at the cost of complexity for the script creator. Once a script is created, though, it can be easily shared with other users.

See the generic description of the scripting languaged used in [the Anko scripting language documentation](scripting.md) for more details about the language itself.

## Managing anko scripts

In order to run an anko script in a search, the text file containing the script must be uploaded as a resource. See the [resources section](#!resources/resources.md) for information on how to create and upload a resource.

At this time, to make a change to a script you must edit the script in the original text file, then re-upload the file to the resource. Future versions of Gravwell will include an integrated text editor to make scripting simpler.

## Running an anko script

To run a script, simply specify "anko", followed by the name of the script, followed by any arguments intended for the script. For example, to run a script named "foo" which takes two numbers as arguments, type `anko foo 1 3` in the pipeline.

## Writing anko scripts

Anko scripts use the same syntax as eval commands; refer to examples below and in the eval module section.

### Essential function definitions

An anko script **must** contain either a function named `Process` or a function named `Main`. These functions do not take arguments. These two functions represent two different options for processing search entries.

If a `Process` function is defined, it will be called once per search entry; enumerated values on the entry may be treated as local variables, and the return value of the `Process` function determines if the entry is allowed to continue down the pipeline (true) or not (false).

If a `Main` function is defined, it will be called only once; the programmer must therefore call the `readEntry` and `writeEntry` functions to fetch each search entry and pass it down the line after operating on it.

We strongly recommend writing scripts with `Process` instead of `Main` whenever possible, because it is conceptually much simpler.

The script may also contain functions named `Parse` and `Finalize`.

The `Parse` function is called before `Process` or `Main` and is given the command line arguments as an array of arguments. The `Parse` function indicates that the arguments have been successfully processed by returning nil; any non-nil return is treated as an error and presented to the user. See the sample script below for a sample of how to parse script arguments.

The `Finalize` function is called after `Process` or `Main` have completed. It is the last code executed in the script; this is a good place to create resources if desired.

### Sample script using Process() function

This example script operates in two modes, specified as an argument to the script. In 'build' mode, it takes the "SrcIP" field extracted from the packet module and builds a list of IP addresses seen in the current search, then stores that list as a resource. In 'apply' mode, it takes the previously-built table and drops any entries which contain a previously-seen "SrcIP" field. This script was used to look for new devices on a network, although the `lookup` module now provides the same functionality with more flexibility.

```
table = make(map[string]interface)
task = "build"

var json = import("encoding/json")

# first arg = "build" or "apply"
func Parse(args) {
	errstr = "argument must be 'build' or 'apply'"
	if len(args) == 1 {
		task = args[0]
	} else {
		return errstr
	}
	switch task {
	case "apply":
		# load the table
		data, _ = getResource("lookuptable")
		json.Unmarshal(data, &table)
	case "build":
	default:
		return errstr
	}
	return nil
}

func Process() {
	if task == "build" {
		s = toString(SrcIP)
		table[s] = true
		return true
	} else if task == "apply" {
		s = toString(SrcIP)
		# create & set an enumerated value named "new" to true or false
		setEnum("new", !table[s])
		# if it's not in the table, return true
		return !table[s]
	}
}

func Finalize() {
	if task == "build" {
		data, err = json.Marshal(table)
		if err != nil {
			return err
		}
		return setResource("lookuptable", data)
	}
}
```

Observe that the "SrcIP" enumerated value may be **read** like any other variable inside the `Process` function, but in order to set an enumerated value we must use the `setEnum` function to make the action explicit.

Note that the `table` and `task` variables are declared outside the function definitions. The built-in json encoding library is also imported prior to the function definitions. A full list of available libraries is provided below.


### Sample script using Main() function

Although writing scripts using a `Main` function is more challenging, it is necessary if you need to duplicate entries. The following script reads in an entry containing a Modbus message; if the message is a request of type 0x10 ("Write multiple registers"), the script duplicates the original entry once for each of the registers being written and to each entry attaches "RegAddr" and "RegValue" enumerated values containing a single register address + register value.

Note: This script will not function on its own; as written, it was intended to consume the output of another anko script earlier in the pipeline, which would populate enumerated values such as "Request" and "WriteAddr".

```
func Main() {
	for i = 0; i != -1; i++ {
		ent, err = readEntry()
		if err != nil {
			return
		}

		# Check if this is a request or a response
		Request, err = getEntryEnum(ent, "Request")
		if err != nil {
			#Request isn't set, this isn't a modbus packet, skip
			continue
		}

		# read the function value
		Function, err = getEntryEnum(ent, "Function")
		if err != nil {
			continue
		}

		ReqResp, err = getEntryEnum(ent, "ReqResp")
		if err != nil {
			continue
		}

		if Request == true {
			if Function == 0x10 {
				# write multiple registers
				Addr, err = getEntryEnum(ent, "WriteAddr")
				if err != nil {
					writeEntry(ent)
					continue
				}
				Count, err = getEntryEnum(ent, "WriteCount")
				if err != nil {
					writeEntry(ent)
					continue
				}
				if Count == 0 || len(ReqResp) < 5 + 2*Count {
					writeEntry(ent)
					continue
				}
				for j = 0; j < Count; j++ {
					newEnt = cloneEntry(ent)
					# read the register value
					val = (toInt(ReqResp[5+(2*j)]) << 8) | toInt(ReqResp[5+(2*j)+1])
					setEntryEnum(newEnt, "RegAddr", Addr + j)
					setEntryEnum(newEnt, "RegValue", val)
					err = writeEntry(newEnt)
					if err != nil {
						continue
					}
				}
			} else {
				writeEntry(ent)
			}
		}
	}
}
```

Note the use of the `readEntry`, `cloneEntry`, and `writeEntry` functions; this explicit management of search entries is not necessary in scripts using `Process` functions. Note also the use of `getEntryEnum` and `setEntryEnum` functions to read enumerated values rather than treating them as variables.

## Utility functions

Anko provides built-in utility functions, listed below in the format `functionName(<functionArgs>) <returnValues>`. The following functions can be used in any anko script:

* `getResource(name) []byte, error` returns the slice of bytes is the content of the specified resource, while the error is any error encountered while fetching the resource.
* `setResource(name, value) error` creates (if necessary) and updates a resource named `name` with the contents of `value`, returning an error if one arises.
* `len(val) int` returns the length of val, which can be a string, slice, etc.
* `toIP(string) IP` converts string to an IP, suitable for comparing against IPs generated by e.g. the packet module.
* `toMAC(string) MAC` converts string to a MAC address.
* `toString(val) string` converts val to a string.
* `toInt(val) int64` converts val to an integer if possible. Returns 0 if no conversion is possible.
* `toFloat(val) float64` converts val to a floating point number if possible. Returns 0.0 if no conversion is possible.
* `toBool(val) bool` attempts to convert val to a boolean. Returns false if no conversion is possible. Non-zero numbers and the strings “y”, “yes”, and “true” will return true.
* `typeOf(val) type` returns the type of val as a string, e.g. “string”, “bool”.

The following functions are only available in scripts implementing the `Process` function:

* `setEnum(key, value) error` creates an enumerated value on the current entry named `key` containing `value`.
* `getEnum(key) value, error` returns the enumerated value specified by `key`
* `delEnum(key)` deletes an enumerated value named `key` from the current entry.
* `hasEnum(key) bool` returns whether the current entry has the enumerated value.

The following functions are only available in scripts implementing the `Main` function:

* `readEntry() entry, error` returns the next entry and an error (if any). It will return an error when no entries remain.
* `writeEntry(ent) error` writes out the given entry down the pipeline, returning an error if any.
* `cloneEntry(ent) entry` returns a copy of the specified entry.
* `setEntryEnum(ent, key, value)` sets an enumerated value on the specified entry.
* `getEntryEnum(ent, key) value, error` reads an enumerated value from the specified entry.
* `hasEntryEnum(ent, key) bool` returns whether the entry contains the enumerated value.
* `delEntryEnum(ent, key)` deletes the specified enumerated value from the given entry.
* `setEntryData(ent, value)` sets the data portion of an entry.

Note: The `setEnum`, `hasEnum`, and `delEnum` functions differ for scripts using `Process` functions vs. `Main` functions, because the `Process` function is implicitly operating on a particular entry.

## Available packages

It is possible to import anko wrappers for certain Go libraries with syntax similar to the following:

```
var json = import("encoding/json")
```

For security reasons, the anko module does not allow access to *all* packages included with the full Anko scripting language. The following packages are available for use in anko scripts:

* `bytes`: work with byte slices
* `crypto/md5`, `crypto/sha1`, `crypto/sha256`, `crypto/sha512`: cryptographic hashing
* `encoding/csv`: encode and decode CSV data
* `encoding/json`: encode and decode json data
* `errors`: handle Go errors
* `flag`: handle command-line arguments
* `fmt`: printing & formatting strings
* `math`: mathematical functions
* `math/big`: bignums
* `math/rand`: random numbers
* `net/http`: limited HTTP functionality (client only)
* `net/url`: URLs
* `path`: paths
* `path/filepath`: path functions specific to files
* `regexp`: regular expressions
* `sort`: sorting
* `strings`: string processing functions
* `time`: time processing functions
* `github.com/ziutek/telnet`: telnet client functions (the Dial, DialTimeout, and NewConn functions are available, see [https://godoc.org/github.com/ziutek/telnet](https://godoc.org/github.com/ziutek/telnet) for documentation.

An exhaustive description of every package is not possible in this document; you can view the available functions exported for each package at [the official anko repository](https://github.com/mattn/anko/tree/master/packages). Some specific packages are described further below, as they do not offer the complete functionality exported by the official anko repository.

### The `net/http` package

`net/http` exports a subset of functions, types, and variables for performing HTTP *requests*. The types `Client`, `Cookie`, `Request`, and `Response` are exported; see [the Go documentation](https://golang.org/pkg/net/http/) for a description of these types.

The function `NewRequest(operation, url, body) (Request, error)` prepares a new http.Request with the given operation ("PUT", "POST", "GET", "DELETE") on the specified URL string. The body is an optional parameter for use with PUT and POST requests; it should be set to either 'nil' or an io.Reader.

For most purposes, you will create a Request with the NewRequest function, then use http.DefaultClient to execute that request:

```
req, _ = http.NewRequest("GET", "http://example.org/foo", nil)
http.DefaultClient.Do(req)
```

Additional headers or cookies can be set on the request before sending:

```
req, _ = http.NewRequest("GET", "http://example.org/foo", nil)
# Add a header
req.Header.Add("My-Header", "gravwell")
# Add a cookie
cookie = make(http.Cookie)
cookie.Name = "foo"
cookie.Value = "bar"
req.AddCookie(&cookie)
http.DefaultClient.Do(req)
```
