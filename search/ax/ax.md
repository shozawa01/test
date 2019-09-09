## AX

ax���W���[���́A���̃��W���[���̋@�\���Ăяo�����Ƃɂ���ăf�[�^����t�B�[���h�𒊏o���邽�߂Ɏ��O���o�K�����g�p���郉�b�p�[���W���[���ł��B���ȋL�q�^�A�W���^�A�܂��͍\��������Ă��Ȃ��f�[�^���g�p����N�G����啝�Ɋȗ����ł��܂��B

�ȉ���AX�v���Z�b�T���g�p�\�ł�:

* [CSV](../csv/csv.md)
* [Fields](../fields/fields.md)
* [Regex](../regex/regex.md)
* [Slice](../slice/slice.md)

AX�G�N�X�g���N�^�̐ݒ�Ɋւ��銮�S�ȃh�L�������g�ɂ��ẮA[autoextractor�Z�N�V����](../../configuration/autoextractors.md)���Q�Ƃ��Ă��������B

### �t�B���^�����O

ax���W���[���́A��b�ƂȂ�v���Z�b�T�Ɠ����t�B���^�����Z�}���e�B�N�X���g�p���āA���o�l�ɑ΂���C�����C���t�B���^�������T�|�[�g���܂��B�e�v���Z�b�T�́A�t�B���^���Z�q�̓���̃T�u�Z�b�g���T�|�[�g�ł��܂��B

���Ƃ��΁ACSV�Afields�A�����regex�v���Z�b�T�́A�����t�������t�B���^�i==�I=?�I?�j���T�|�[�g���Ă��܂��B�X���C�X�v���Z�b�T�́A�L���X�g�̎�ނɉ����ē���̃t�B���^���T�|�[�g���܂��B

| �I�y���[�^�[ | �� | ���� |
|----------|------|-------------|
| == | ������ | �t�B�[���h�͓������Ȃ���΂Ȃ�܂���
| != | �������Ȃ� | �t�B�[���h�͓������Ă͂����܂���
| ~ | �T�u�Z�b�g | �t�B�[���h�ɒl���܂܂�Ă��܂�
| !~ | �T�u�Z�b�g�ł͂Ȃ� | �t�B�[���h�ɒl���܂܂�Ă��܂���
| < | ���� | �t�B�[���h�̐��l����菬����
| <= | ��菬������������ | �t�B�[���h�̐��l���ȉ��ł���
| > | ���傫�� | �t�B�[���h�̐��l�����傫��
| >= | �ȏ� | �t�B�[���h�̐��l���ȏ�

���F���ׂẲ��Z�q�����ׂẴv���Z�b�T�[�ŃT�|�[�g����Ă���킯�ł͂���܂���B�����̃^�O���������O�̃t�B�[���h�𒊏o����ƁA�t�B���^���Z�q�Z�b�g�͋��ʂ̃T�u�Z�b�g�ɐ�������܂��B

### AX�̋N��

AX���W���[���́A�����̃J�X�^���v���Z�b�T�œ����ɕ����̃^�O�������ł��܂��B  �܂�ACSV�f�[�^���܂� "foo"�Ƃ����^�O�ƁA��\�����f�[�^���܂� "bar"�Ƃ����^�O������ꍇ�́Aax���g�p���ė����̃X�g���[����1��̌Ăяo���ŃV�[�����X�ɏ����ł��܂��B  ����́A2�̈قȂ�f�[�^�`���iCSV�Ɣ�\�����j�̗�ł�:

```
2019-02-07T14:39:21.819693-07:00,cotton,59296,6accf07c-d7fb-4394-b27c-a8fde782e4a7,111.63.178.212,2697,115.152.163.129,1381
2019-02-07T14:39:29.529007-07:00 [calico] <7dee02fa-06a7-493d-812b-54f0d9a33b2b> 7e2:d377:3b3e:669d:b2f9:d311:b99f:f1d6 4462 7a38:8702:357b:9e09:e9ad:959d:1e1a:949 557
```

CSV�f�[�^�ɂ́utestcsv�v�Ƃ����^�O���t�����A��\�����f�[�^�ɂ́utestregex�v�Ƃ����^�O���t������Ƒz�肵�܂��B 2�̃f�[�^�`���͑傫���قȂ�܂����A�������̋��ʃf�[�^�t�B�[���h���܂܂�Ă��܂��B �f�[�^�t�H�[�}�b�g���ƂɁA���̎������o��`���g�p�ł��܂�:

```
[[extraction]]
	name="regex"
	module="regex"
	tag="testregex"
	params='(?P<ts>\S+)\s\[(?P<app>\S+)\]\s<(?P<uuid>\S+)>\s(?P<src>\S+)\s(?P<srcport>\d+)\s(?P<dst>\S+)\s(?P<dstport>\d+)'

[[extraction]]
	name="csv"
	module="csv"
	tag="testcsv"
	params="ts, app, id, uuid, src, srcport, dst, dstport"
```

AX��ax���W���[�����g�p���āA�����̃^�O�i "testregex"�� "testcsv"�j���w�肵�ċ��ʃt�B�[���h�𒊏o���A������P��̃r���[�ɓ������邱�Ƃ��ł��܂�:

```
tag=testregex,testcsv ax app src dst | ip src as IP | subnet IP /3 | count by subnet | sort by count desc | table -nt subnet count
```

![Subnet Counts](subcounts.png)

AX�͈�����K�v�Ƃ��܂���B  ax�Ɉ������^�����Ă��Ȃ��ꍇ�A���W���[���͒��o�Ŏw�肳�ꂽ���ׂẴt�B�[���h�𒊏o���܂��B  �������o�ݒ��������2�̃f�[�^�Z�b�g���l����ƁA���ɒP���ȃN�G���𔭍s�ł��܂�:

```
tag=testregex,testcsv ax | table
```

![AX Extract All](ax.png)

�^����ꂽ�t�B���^�Ɉ�v����G���g���������~�����Ƃ������Ƃ��w�肷�邽�߂Ƀt�B���^�����O��ǉ����邱�Ƃ��ł��܂�:

```
tag=testregex,testcsv ax dstport==80 | table app src dst
```

![AX Extract Filter](axfilter.png)
