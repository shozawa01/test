# IPexist

ipexist���W���[���́AIP�A�h���X�̊ȒP�ȑ��݃`�F�b�N���ł��邾���������s����悤�ɐ݌v����Ă��܂��B   Gravwell��[ipexist���C�u����](https://github.com/gravwell/ipexist)���g�p����IP�A�h���X�̃Z�b�g���Ǘ����A���̃Z�b�g���̓����IP�̑��݂����΂₭�Ɖ�܂��B   ���[�U�[�́A�Z�b�g�Əƍ����邽�߂�1�ȏ�̗񋓒l���w�肵�܂��B   �f�t�H���g�ł́A�񋓂��ꂽ���ׂĂ̒l���Z�b�g���̃A�h���X�ƈ�v����ƁA�G���g�����n����܂��B

## �T�|�[�g����Ă���I�v�V����

* `-r <resource>`: "-r"�t���O�́Aipexist�`���̃��b�N�A�b�v�Z�b�g���܂ރ��\�[�X�̖��O���w�肵�܂��B   ���̃t���O�́A�����̃��\�[�X�ɂ܂������Č��������݂邽�߂ɕ�����w�肷�邱�Ƃ��ł��܂��B   �����̃Z�b�g�̍쐬�Ɋւ���ڍׂɂ��ẮA���L���Q�Ƃ��Ă��������B
* `-v`: "-v"�t���O�́Aipexist���W���[���ɋt���[�h�œ��삷��悤�Ɏw�����܂��B   ���������āA�N�G��ipexist -r ips SrcIP���ʏ�ASrcIP�����\�[�X����ip�ƈ�v���邷�ׂẴG���g����ʉ߂�����ꍇ�Aipexist -v -r ips SrcIP�͑���ɂ����̃G���g�����폜���A���̂��ׂẴG���g����ʉ߂����܂��B
* `-or`: "-or"�t���O�́A���ׂẴt�B���^�����������ꍇ�ɁAipexist���W���[�����G���g�����p�C�v���C���ɉ����đ��s���邱�Ƃ������邱�Ƃ��w�肵�܂��B

## IP�Z�b�g���쐬����

ipexist���W���[���͓���̃t�H�[�}�b�g���g�p����IPv4�A�h���X�̃Z�b�g���i�[���܂��B  ����́A�����������\�ɂ��Ȃ���A��r�I�X�y�[�X�������ێ�����悤�ɐ݌v����Ă��܂��B  ���̌`���́A�R�}���h���C���ŃZ�b�g�𐶐����邽�߂̃c�[�����܂�[ipexist���C�u����](https://github.com/gravwell/ipexist)�Ɏ�������Ă��܂��B

�܂��A�c�[�����擾���܂�:

	go get github.com/gravwell/ipexist/textinput

���ꂩ��A�Z�b�g�ɓ��ꂽ��IP�A�h���X�̃��X�g��1�s��1��IP�A�h���X�Ńe�L�X�g�t�@�C���ɓ��͂��Ă��������B  �����͊֌W����܂���:

	10.0.0.2
	192.168.3.77
	10.3.2.1
	8.8.8.8

����textinput�c�[�������s���A���̓t�@�C���ւ̃p�X�Əo�͂ւ̃p�X���w�肵�܂�:

	$GOPATH/bin/textinput -i /path/to/inputfile -o /path/to/outputfile

����ɂ��Aipexist���W���[���Ŏg�p���邽�߂̃��\�[�X�Ƃ��ăA�b�v���[�h�ł���K�؂Ƀt�H�[�}�b�g���ꂽ�o�̓t�@�C�����쐬����܂��B

## �g�p��

�p�P�b�g��pcap�^�O�̉��ŃL���v�`�������Ɖ��肷��ƁA���̃N�G���̓\�[�XIP�A�h���X��ips���\�[�X����IP�ƈ�v����p�P�b�g�݂̂�ʉ߂����܂�:

```
tag=pcap packet ipv4.SrcIP | ipexist -r ips SrcIP | table SrcIP
```

![](ipexist1.png)

���̃N�G���́ASrcIP��DstIP�����\�[�X�ɂ���G���g�������ׂēn���܂�:

```
tag=pcap packet ipv4.SrcIP ipv4.DstIP | ipexist -r ips SrcIP DstIP | table SrcIP DstIP
```

`-or`�t���O��ǉ�����ƁA�Ɖ�ɘa����܂��B   SrcIP�܂���DstIP�����\�[�X�Ɍ��������G���g�������ׂēn���܂�:

```
tag=pcap packet ipv4.SrcIP ipv4.DstIP | ipexist -or -r ips SrcIP DstIP | table SrcIP DstIP
```

## ���]�N�G��

`-v`�t���O�̓N�G���𔽓]���܂��B  �N�G����-v��ǉ������ꍇ�A�ʏ�폜�����G���g���͂��ׂēn����A���̋t�����l�ł��B

���̃N�G���́A�\�[�XIP�A�h���X�����\�[�X���Ɍ��������G���g�����폜���܂�:

```
tag=pcap packet ipv4.SrcIP | ipexist -v -r ips SrcIP | table SrcIP
```

![](ipexist2.png)

���̃N�G���ł́ASrcIP��DstIP�����\�[�X�ɑ��݂���G���g���͂��ׂč폜����܂��B   ���̖₢���킹�͖{���I�ɁA�u���M���܂��͈��悪���m�̃��X�g�ɂȂ����ׂẴp�P�b�g��\������v�ƂȂ�܂��B

```
tag=pcap packet ipv4.SrcIP ipv4.DstIP | ipexist -v -r ips SrcIP DstIP | table SrcIP DstIP
```

`-or`�t���O�Ƒg�ݍ��킹��ƁA���W���[���́A�w�肳�ꂽ�񋓒l��1�ł����\�[�X���Ɍ��������G���g�������ׂč폜���܂��B   �ȉ��̗�ł́A�\�[�XIP�ƈ���IP�����\�[�X�Ɍ�����Ȃ��G���g���������p�C�v���C����ʉ߂��܂��B

```
tag=pcap packet ipv4.SrcIP ipv4.DstIP | ipexist -or -r ips SrcIP DstIP | table SrcIP DstIP
```

### �����̃��\�[�X

`-r`�t���O���J��Ԃ����Ƃɂ���āA�����̌ŗLIP�Z�b�g���w��ł��܂��B   ipexists���W���[���͖{���I�ɂ�����1�̑傫�ȃZ�b�g�Ƃ��Ĉ����܂��B

```
tag=pcap packet ipv4.SrcIP | ipexist -r ips -r externalips SrcIP | table SrcIP
```
