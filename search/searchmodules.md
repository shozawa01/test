# Search Modules

�������W���[���́A�p�X�X���[���[�h�Ńf�[�^���������郂�W���[���ł��B  �܂�A�������W���[���͉��炩�̃A�N�V�����i�t�B���^�A�ύX�A���בւ��Ȃǁj�����s���A�G���g�����p�C�v���C���ɓn���܂��B  �������W���[���͑������݂���\��������A���ꂼ�ꂪ�Ǝ��̌y�ʃX���b�h�œ��삵�܂��B  �܂�A������10�̃��W���[��������ꍇ�A�p�C�v���C����10�̃X���b�h���g�p���ĕ��U���܂��B  �e���W���[���̃h�L�������g�́A���̃��W���[���ɂ���ĕ��U�������܂肽���܂ꂽ��\�[�g���ꂽ�肷�邩�ǂ����������܂��B  ���W���[�������󂷂�ƁA���U�p�C�v���C���͋����I�ɕ��󂵂܂��B  �܂�A���W���[���Ƃ��ׂẴ_�E���X�g���[�����W���[���̓t�����g�G���h�Ŏ��s����܂��B  �������J�n����Ƃ��́A�ŏ��̐܂肽���݃��W���[���̏㗬�ɂł��邾�������̕��񃂃W���[����z�u���āA�ʐM�p�C�v�ւ̕��S���y�����A���傫�ȕ��񏈗����\�ɂ��邱�Ƃ��őP�ł��B

## ���j�o�[�T���t���O

���L�̃t���O�͂������̈قȂ錟�����W���[���Ԃŋ��ʂ��Ďg�p���邱�Ƃ��ł��܂��B:

* `-e <source name>` ���W���[�����G���g���̃f�[�^�t�B�[���h����ł͂Ȃ��A�w�肳�ꂽ�񋓒l������̓f�[�^��ǂݎ�낤�Ƃ��邱�Ƃ��w�肵�܂��B����́AJSON�G���R�[�h���ꂽ�f�[�^�����傫�ȃf�[�^���R�[�h���璊�o���ꂽ�\��������json�̂悤�ȃ��W���[���ɖ𗧂��܂��B���Ƃ��΁A���̌�����HTTP�p�P�b�g�̃y�C���[�h����JSON�t�B�[���h��ǂݍ������Ƃ��܂�: `tag=pcap packet tcp.Payload | json -e Payload user.email`
* `-t <target name>` ���W���[�����\�[�X���㏑������̂ł͂Ȃ��A�w�肳�ꂽ���O�̗񋓒l�ɏo�͂��������ނ悤�Ɏw�肵�܂��B���Ƃ��΁A[hexlify](hexlify/hexlify.md)���W���[���͒ʏ�A16�i�G���R�[�h���ꂽ�o�͕�������G���g���̃f�[�^�t�B�[���h�ɏ����߂��܂����A`-t`�t���O���w�肳��Ă���ꍇ�́A����Ƀ\�[�X�����̂܂܂ɂ��Ė��O�t���񋓒l�ɏo�͂��������݂܂��B
* `-r <resource name>` [resources](#!resources/resources.md)�V�X�e�����̃��\�[�X���w�肵�܂��B����͒ʏ�A[geoip](geoip/geoip.md)���W���[�����g�p����GeoIP�}�b�s���O�e�[�u���ȂǁA���W���[�����g�p����ǉ��f�[�^��ۑ����邽�߂Ɏg�p����܂�
* `-v` �ʏ�̃p�X/�h���b�v���W�b�N�𔽓]����K�v�����邱�Ƃ������܂��B�Ⴆ�΁A[grep](grep/grep.md)���W���[���͒ʏ�A�^����ꂽ�p�^�[���Ƀ}�b�`����G���g����n���A�}�b�`���Ȃ����̂��폜���܂��B`-v`�t���O���w�肷��ƁA��v����G���g�����폜���A��v���Ȃ��G���g����n���܂��B
* `-s` "������"���[�h�������܂��B�������̏����̂����̂ǂꂩ1�ł���������Ă���ꍇ�A���W���[�����ʏ�G���g�����p�C�v���C����i�ނ��Ƃ�������ꍇ�Astrict�t���O��ݒ肷�邱�Ƃ́A���ׂĂ̏������������ꂽ�ꍇ�ɂ̂݃G���g�����i�ނ��Ƃ��Ӗ����܂��B���Ƃ��΁A[require](require/require.md)���W���[���͒ʏ�A�K�v�ȗ񋓒l�̂����ꂩ���܂܂�Ă���ꍇ��`-s`�G���g����n���܂����A�t���O���g�p����Ă���ꍇ�́A�w�肳�ꂽ*���ׂ�*�̗񋓒l���܂ރG���g���݂̂�n���܂��B

## ���j�o�[�T���񋓒l

���ׂĂ̌������W���[���ɂ́A���R�[�h�̃��j�o�[�T���񋓒l������܂�

* SRC -- �G���g���f�[�^�̃\�[�X
* TAG -- �G���g���ɓY�t����Ă���^�O
* TIMESTAMP -- �G���g���̃^�C���X�^���v
* DATA -- ���ۂ̃G���g���f�[�^

�����̓��[�U�[��`�̗񋓒l�Ɠ����悤�Ɏg�p�ł��܂��B

## �������W���[���̏ڍ�

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
