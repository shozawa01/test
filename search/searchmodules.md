# Search Modules

Search modules are modules that operate on data in a passthrough mode, meaning that they perform some action (filter, modify, sort, etc.) and pass the entries down the pipeline. There can be many search modules and each operates in its own lightweight thread.  This means that if there are 10 modules in a search, the pipeline will spread out and use 10 threads.  Documentation for each module will indicate if the module causes distributed searches to collapse and/or sort.  Modules that collapse force the distributed pipelines to collapse, meaning that the module as well as all downstream modules execute on the frontend.  When starting a search it's best to put as many parallel modules as possible upstream of the first collapsing module, decreasing pressure on the communication pipe and allowing for greater parallelism.

## Universal Flags

Some flags appear in several different search modules and have the same meaning throughout:

* `-e <source name>` specifies that the module should attempt to read its input data from the given enumerated value rather than from the entry's data field. This is useful in for modules like [json](json/json.md), where the JSON-encoded data may have been extracted from a larger data record, for example the following search will attempt to read JSON fields from the payloads of HTTP packets: `tag=pcap packet tcp.Payload | json -e Payload user.email`
* `-t <target name>` specifies that the module should write its output to an enumerated value with the given name, rather than overwriting the source. For example, the [hexlify](hexlify/hexlify.md) module will normally write its hex-encoded output string back to the entry's data field, but if the `-t` flag is given, it will instead leave the source intact and write its output to the named enumerated value.
* `-r <resource name>` specifies a resource in the [resources](#!resources/resources.md) system. This is generally used to store additional data used by the module, such as a GeoIP mapping table used by the [geoip](geoip/geoip.md) module.
* `-v` indicates that the normal pass/drop logic should be inverted. For example the [grep](grep/grep.md) module normally passes entries which match a given pattern and drop those which do not match; specifying the `-v` flag will cause it to drop entries which match and pass those which do not.
* `-s` indicates a "strict" mode. If a module normally allows an entry to proceed down the pipeline if any one of several conditions are met, setting the strict flag means an entry will proceed only if *all* conditions are met. For example, the [require](require/require.md) module will normally pass an entry if it contains any one of the required enumerated values, but when the `-s` flag is used, it will only pass entries which contain *all* specified enumerated values.

## Universal Enumerated Values

Every search module has universal enumerated values for records.

* SRC -- the source of the entry data.
* TAG -- the tag attached to the entry.
* TIMESTAMP -- the timestamp of the entry.
* DATA -- the actual entry data.

These can be used just like user-defined enumerated values.

## Search module documentation

* [abs](abs/abs.md)
* [alias](alias/alias.md)
* [anko](anko/anko.md)
* [ax](ax/ax.md)
* [base64](base64/base64.md)
* [canbus](canbus/canbus.md)
* [cef](cef/cef.md)
* [count](math/math.md#Count)
* [csv](csv/csv.md)
* [entropy](math/math.md#Entropy)
* [eval](eval/eval.md)
* [fields](fields/fields.md)
* [geoip](geoip/geoip.md)
* [grep](grep/grep.md)
* [hexlify](hexlify/hexlify.md)
* [ip](ip/ip.md)
* [ipexist](ipexist/ipexist.md)
* [ipfix](ipfix/ipfix.md)
* [j1939](j1939/j1939.md)
* [join](join/join.md)
* [json](json/json.md)
* [langfind](langfind/langfind.md)
* [length](length/length.md)
* [limit](limit/limit.md)
* [lookup](lookup/lookup.md)
* [lower](upperlower/upperlower.md)
* [Math (list of math modules)](math/math.md)
* [max](math/math.md#Max)
* [mean](math/math.md#Mean)
* [min](math/math.md#Min)
* [namedfields](namedfields/namedfields.md)
* [netflow](netflow/netflow.md)
* [packet](packet/packet.md)
* [packetlayer](packetlayer/packetlayer.md)
* [regex](regex/regex.md)
* [require](require/require.md)
* [slice](slice/slice.md)
* [sort](sort/sort.md)
* [src](src/src.md)
* [stats](stats/stats.md)
* [stddev](math/math.md#Stddev)
* [strings](strings/strings.md)
* [subnet](subnet/subnet.md)
* [sum](math/math.md#Sum)
* [syslog](syslog/syslog.md)
* [taint](taint/taint.md)
* [unique](math/math.md#Unique)
* [upper](upperlower/upperlower.md)
* [variance](math/math.md#Variance)
* [winlog](winlog/winlog.md)
* [xml](xml/xml.md)
