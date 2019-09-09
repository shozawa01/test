# Math Modules

math���W���[���́A�p�C�v���C����œ��삵�ē��v���͂����s���܂��B  �܂��A�^�C�����C���ŏ�񂪋Ïk�����ꍇ�ɂ��d�v�ł��B  ���Ƃ��΁A���x��1�b������10�񑪒肳��Ă��邪�A���[�U�[��1�b���Ƃɕ\������悤�ɗv�������ꍇ�Amath���W���[�����g�p���Ă��̃f�[�^�����k���܂��B

## Sum

sum���W���[���̓��R�[�h�̒l�����Z���܂��B  ����̓f�t�H���g�̓���ł���A���ڌĂяo����邱�Ƃ͂����炭�Ȃ��ł��傤�B

MAC�A�h���X���l�b�g���[�N��ő��M�����f�[�^���܂Ƃ߂�������:

```
tag=pcap eth.SrcMAC eth.Length | sum Length by SrcMAC | chart sum by SrcMAC
```

## Mean

mean���W���[���̓��R�[�h�̕��ϒl��Ԃ��܂��B
�ԗ���RPM�`���[�g�̌����`���[�g�̗�:

```
tag=CAN canbus ID=0x2C4 | slice uint16BE(data[0:2]) as RPM | mean RPM | chart mean
```

## Count

Count���W���[���̓��R�[�h�̃C���X�^���X���J�E���g���܂��B  ���R�[�h���̃f�[�^�ɑ΂��ĎZ�p���Z���s���܂���B

Linux�}�V�������sudo�R�}���h�̃J�E���g��:

```
grep sudo | regex "COMMAND=(?P<command>\S+)" | count by command | chart count by command
```

����́A�l�b�g���[�N���MAC�A�h���X�ɂ���đ��M���ꂽ�p�P�b�g�̐�������������ł��isum���W���[���̗�Ɏ�����Ă���悤�ɁA�e�p�P�b�g�̃T�C�Y�Ƃ͈قȂ�܂��j:

```
tag=pcap eth.SrcMAC eth.Length | sum Length by SrcMAC | chart sum by SrcMAC
```

## Max

max���W���[���͍ő�l��Ԃ��܂��B

�t���[�g�S�̂̊e�ԗ��̍ő�RPM�̕\������������:

```
tag=CAN canbus ID=0x2C4 | slice uint16BE(data[0:2]) as RPM | max RPM by SRC | table SRC max
```

## Min

min���W���[���͍ŏ��l��Ԃ��܂��B

�t���[�g�S�̂̊e�ԗ��̍ŏ�RPM�̕\������������:

```
tag=CAN canbus ID=0x2C4 | slice uint16BE(data[0:2]) as RPM | min RPM by SRC | table SRC min
```

## Variance

Variance���W���[���́A���R�[�h�̕��U����Ԃ��܂��B  ����͕ω�������������̂ɖ𗧂��܂��B

�g���^�Ԃ̃X���b�g���f�[�^�̕��U���O���t������������:

```
tag=CAN canbus ID=0x2C1 | slice byte(data[6:7]) as throttle | variance throttle | chart variance
```

## Stddev

�W���΍�

stddev���W���[���̓��R�[�h�̕W���΍�����Ԃ��܂��B  ����ُ͈�ȃC�x���g����������̂ɖ𗧂��܂��B

�O��l�ł���RPM�M�����O���t������������:

```
tag=CAN canbus ID=0x2C4 | slice uint16BE(data[0:2]) as RPM | stddev RPM | chart stddev
```

## Unique

unique���W���[���́A�N�G���f�[�^���̏d���G���g����r�����܂��B  �P��unique���w�肷��ƁA�e�G���g���̃f�[�^�̃n�b�V���Ɋ�Â��ďd���G���g�����`�F�b�N����܂��B   1�ȏ�̗񋓒l�̖��O���w�肷��ƁAunique���񋓒l�݂̂��t�B���^�����O���܂��B  �Ⴂ�͎��̂悤�ɐ����ł��܂�:

```
tag=pcap packet tcp.DstPort | unique
```

```
tag=pcap packet tcp.DstPort | unique DstPort
```

�ŏ��̖₢���킹�̓p�P�b�g�̓��e�S�̂����邱�Ƃɂ���ďd�������p�P�b�g�����O���܂��B  �p�P�b�g�͒ʏ�V�[�P���X�ԍ��̂悤�Ȃ��̂��܂�ł���̂ŁA����͑�����B�����Ȃ��ł��傤�B   2�Ԗڂ̃N�G���́A���o���ꂽDstPort�񋓒l���g�p���Ĉ�Ӑ����e�X�g���܂��B  ����͂܂�TCP�|�[�g80���Ă̍ŏ��̃p�P�b�g�͒ʉ߂��܂����A�|�[�g80���Ă̂���ȍ~�̃p�P�b�g�͂��ׂăh���b�v����܂��B

�����̈������w�肷��ƁAunique�͂����̈����̂��ꂼ��ŗL�̑g�ݍ��킹��T���܂��B

```
tag=pcap packet tcp.DstPort tcp.DstIP | eval DstPort < 1024 | unique DstPort DstIP | table DstIP DstPort
```

��L�̌����ł́A�|�[�g��1024�����ł���΁AIP +�|�[�g�̂��ׂĂ̌ŗL�̑g�ݍ��킹���o�͂���܂��B  ����́A���Ƃ��΃l�b�g���[�N��̃T�[�o�[��������̂ɕ֗��ȕ��@�ł��B

## Entropy

Entropy���W���[���́A�t�B�[���h�l�̃G���g���s�[���o���I�Ɍv�Z���܂��B  �����Ȃ��ŃG���g���s�[���w�肷��ƁA�����͈͑S�̂̂��ׂẴG���g���[�̃f�[�^�Z�N�V�����̃G���g���s�[����������܂��B  �G���g���s�[���W���[���́A�o���I�ȃG���g���s�[�̐}�\�����\�ɂ��鎞�ԓI�������[�h���T�|�[�g����B  �G���g���s�[�͑��̐��w���W���[���Ɠ��l�ɕ����̃L�[���g�p���ė񋓂��ꂽ�l��O���[�v�𑀍삷�邱�Ƃ��ł��܂��B  �G���g���s�[�o�͒l��0����1�̊Ԃł��B

�|�[�g�Ɋ�Â���TCP�p�P�b�g�y�C���[�h�̃G���g���s�[���v�Z���ă`���[�g�ɂ���N�G���̗�:

```
tag=pcap packet tcp.Port tcp.Payload | entropy Payload by Port | chart entropy by Port
```

�z�X�g���Ƃ�URL�̃G���g���s�[���v�Z���A�ł������G���g���s�[�l�Ɋ�Â��ă��X�g���\�[�g����N�G���̗�:

```
tag=pcap packet tcp.Port==80 ipv4.IP !~ 10.0.0.0/8 tcp.Payload | grep -e Payload GET PUT HEAD POST | regex -e Payload "[A-Z]+\s(?P<url>\S+)\sHTTP\/" | entropy url by IP | table IP entropy
```
