# Stats Module

���v���W���[���́A�X�̐��w���W���[����1�̑��삾�������s����ꍇ�ɁA���[�U�[�������ɕ����̓��v��������s���邱�Ƃ��\�ɂ��܂��B  stats���W���[���̕W���I�ȗ�́A�G���[�o�[���O���t�ɕ\�����邽�߂ɒl�̕��ςƕW���΍����v�Z���邱�Ƃł��B

## �\��

stats���W���[���̌Ăяo���́A���̂��̂ō\������Ă��܂�:

* ���W���[���� (`stats`)
* �ǂ̗񋓒l�𑀍삷�邩���w�肷�鑀��̃��X�g�A����уI�v�V�����ŏo�̖͂��O (`mean(length)`, `count as foo`)
* �I�v�V������"by"�����Bby�����̊e�g�ݍ��킹�ɑ΂��ČʂɎ��s���邱�Ƃ��w�肵�܂��i `mean�iLength�jby SrcIP`�̂悤�Ɂj

�����̍\���v�f�ɂ��Ă͌�q���܂��B

## ���w���Z�d�l
 
����́A���얼�A���ʓ��Ɋ܂܂��"�\�[�X"�񋓒l�A����уI�v�V�����ŏo�͗񋓒l�̕ʂ̖��O�ō\������܂��B

�ȉ��̑��얼���T�|�[�g����Ă��܂�:

* count: �G���g����
* sum: ���v�����l��Ԃ�
* mean: ���ϒl���v�Z����
* stddev: �W���΍����v�Z����
* variance: ���U���v�Z����
* min: �ŏ��l��Ԃ�
* max: �ő�l��Ԃ�

����̓\�[�X�񋓒l�ɑ΂��Ď��s����܂��B  ���������āA�w��`stats sum(Bytes)`����ƁAstats���W���[����Bytes�񋓒l�����v��`sum`�A���v���܂ނƂ������O�̗񋓒l�����P��̃G���g�����o�͂���悤�Ɏw������܂��B

���F�\�[�X���w�肳��Ă��Ȃ��ꍇ�́A����ɃG���g���[�̖{�̂ɑ΂��đ��삪���s����܂��B  �w��stats sum���邱�Ƃ�`stats sum(DATA)`���w�肷�邱�ƂƓ����ł�

�����̑�����w��ł��܂�:

```
stats sum(Bytes) mean(Bytes)
```

```
stats mean(Bytes) stddev(bytes) min(Length)
```

�I�y���[�V�����̏o�͂́A�f�t�H���g�ł́A�I�y���[�V�����̖��O�ƂƂ��ɗ񋓒l�Ɋ��蓖�Ă��܂��B  ���������āA`stats sum�iBytes�j`�́A�o�͂�ێ����邽�߂�`sum`�Ƃ������O�̗񋓒l���쐬���܂��B  �����`as`�I�v�V�����ŕύX�ł��܂��F

```
stats mean(Bytes) as BytesAvg
```

����́A�����̈قȂ�񋓒l�ɑ΂��ē�����������s����Ƃ��ɓ��ɕ֗��ł�:

```
stats mean(Bytes) as BytesAvg mean(Length) as LengthAvg
```

## "By"�����̎w��

���[�U���قȂ�IP���ƂɕʁX�Ɏ��s����鑀���K�v�Ƃ���ꍇ�́A"by����"���w�肷��K�v������܂��B

```
stats mean(Bytes) stddev(Bytes) by SrcIP
```

����́A�e�ŗL��SrcIP�l�ɂ��ĕʁX�̕��ϒl�ƕW���΍����v�Z����悤��stats���W���[���Ɏw�����܂��B  ���ʂ́A������eSrcIP�ɑ΂���1�G���g���ɂȂ�A���ꂼ��ɓK�؂�SrcIP�A���ϒl�A�����stddev�񋓒l���܂܂�܂��B

�K�v�Ȃ��������Ŏw��ł��܂�:

```
stats mean(Bytes) stddev(Bytes) by SrcIP DstIP DstPort
```

���W���[���́ASrcIP�ADstIP�A�����DstPort�̂��ׂĂ̑g�ݍ��킹�ɑ΂��āA�ʁX�̕��ςƕW���΍����v�Z���܂��B

�d�v�F�������[�������Ă���V�X�e���Ŕ��ɑ傫�ȃf�[�^�Z�b�g�������ꍇ�Astats���W���[�������S�����̑g�ݍ��킹���������[���ɕێ����悤�Ƃ��邽�߁A�����ő�������w�������ƃ������[�s���ɂȂ���\��������܂��B

### ���G��"By"�����̎g�p

�P���"by"�����݂̂��񋟂���A���ꂪ�Ō�̑���ɓK�p�����ꍇ�A���v���͂��ׂĂ̑���ɓK�p����܂��B ����͊ȒP�ȕ��@�ł��B���ׂĂ̑���ɓK�p�������Ȃ��ꍇ�́A�Ō�̑����"by"�������Ȃ����Ƃ��m�F���Ă��������B

���Ƃ��΁A�ȉ���`SrcIP DstIP DstPort`���L�[�Ƃ��Ďg�p����"mean"��������s���܂����Astddev����̓L�[�Ȃ��œK�p����܂�:

```
stats mean(Bytes) by SrcIP DstIP DstPort stddev(Bytes)
```

stats���W���[���͕��G�ȃL�[�C���O���g�p���đ�������s�ł��܂��B �܂�A���ׂĂ̑���ɑ΂��ăL�[�Z�b�g�i�܂��̓L�[�Z�b�g�̌��@�j��񋟂ł��܂��B  ����́A�P��̃e�[�u���܂��̓`���[�g�ňقȂ�L�[���g�p���ĕ����̑����\������ꍇ�ɕ֗��ł��B

���Ƃ��΁AIP���Ƃ̃p�P�b�g�T�C�Y�̍��v�����s���邪�A���ׂẴp�P�b�g�̃x�[�X���C�����v���񋟂���N�G���͎��̂Ƃ���ł�:

```
tag=pcap packet ipv4.IP ~ 10.10.10.0/24 | length | stats sum(length) by IP sum(length) as total | chart total sum by IP 
```

![complex keys](complexkey.png)

## �^�C���E�B���h�E�̎w��

stats���W���[���́Acondensed�܂���temporal��2�̃��[�h�œ���ł��܂��B

condensed���[�h�ł́A���ʂ�1�񂾂��o�͂��܂��B  ����́A�e�L�X�g�����_���[�̎g�p���A�܂��̓e�[�u�������_���[��`-nt`�t���O���n���ꂽ�Ƃ��Ɏ����I�ɔ������܂��B

temporal���[�h�ł́Astats���W���[���͎��Ԙg�œ��삵�A�f�t�H���g��1�b�ł��B  �f�[�^��1�b���ƂɁA���W���[���͌��ʃG���g���̃Z�b�g�𔭍s���܂��B  ����́A�f�[�^���`���[�g�����_���[�ɑ��M����Ƃ��Ɏg�p����܂��B

�f�t�H���g�̃E�B���h�E��1�b�ł����A�E�B���h�E�T�C�Y��"over"�I�v�V�����ŕύX�ł��܂�:

```
stats mean(Bytes) stddev(Bytes) by SrcIP over 5m
```

�`���[�g���W���[���ɑ��M�����ƁA���ʂ͕W����1�b�ł͂Ȃ�5���ԂŌv�Z����܂��B

���F�w��ł��鎞�Ԙg��1�����ŁA���̎��Ԙg�͂��ׂĂ̑���ɓK�p����܂��B  timewindow�́Astats��LAST�����ł�����K�v������܂�