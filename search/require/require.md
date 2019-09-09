# Require

require���W���[���́A�p�C�v���C�����̃G���g���𒲂ׂāA����̗񋓌^�t�B�[���h�������Ȃ��G���g�����폜����P���ȃt�B���^�ł��B  ���[�X�P�[�X�̗�́A�A�b�v�X�g���[�����W���[�������^�f�[�^�𒊏o���Ă��邪�A�K�v�Ȃ��ׂĂ̖��O����ɓ��͂���Ƃ͌���Ȃ��ꍇ�̑�2���x���̃t�B���^�����O�ł��B  [�K�{]��I������ƁA���ۂɖړI�̋@�\�Z�b�g�����G���g���݂̂����W���[����ʉ߂���悤�Ɍ�������܂��B

�f�t�H���g�ł́A�񋓒l�̃��X�g���w�肷��ƁArequire���W���[���́A�񋓒l�̖��O�̂������Ȃ��Ƃ�1���܂܂�Ă���΁A�G���g�����p�C�v���C���ɓn���܂��B  ���̓���́A���Ɏ����悤�Ƀt���O���g���ĕύX�ł��܂��B

## �T�|�[�g����Ă���I�v�V����

* `-s`: `-s`���̃I�v�V�����͌����ȑ�����w�肵�܂��B  �񋓂��ꂽ�񋓒l�́A1�����ł͂Ȃ����ׂđ��݂��Ȃ���΂Ȃ�܂���B  ��{�I�ɁA���W���[����_��OR���Z����_��AND�ɕύX���܂��B
* `-v `: `-v`�I�v�V�����́A�{���I�Ɂu�����̗񋓒l�̂����ꂩ�������ׂẴG���g�����폜����v�ƌ����āA�v�����W�b�N���t�ɂ��܂��B  ���̃t���O�̓t���O���Ӗ���-s�܂��B  �㗬�̃��W���[�������炩�̃t�B�[���h�𒊏o���邩������Ȃ����A���Ȃ���������Ȃ��A�����Ă��Ȃ����t�B�[���h�������Ă��Ȃ������G���g���[�������������Ƃ��A�v�����W���[�����t�ɂ��邱�Ƃ͖��ɗ����Ƃ��ł��܂��B

## �g�p��

���̌����̓p�P�b�g�G���g�����擾���A "SrcPort"�񋓒l���ݒ肳��Ă��Ȃ����̂��폜���Ă���A�e���M���|�[�g���o�������񐔂��J�E���g���܂��B  �����TCP�g���t�B�b�N�ł͂Ȃ����ׂẴp�P�b�g��r��������ʂ�����܂�:

```
tag=pcap packet tcp.SrcPort | require SrcPort | count by SrcPort | table SrcPort count
```

���̌����ł́AA�t�B�[���h���񋓒l�ɑ��݂��邷�ׂẴG���g�����폜���邱�Ƃɂ���āAIPv4�������������Ȃ�����DNS�v����T���܂�:

```
tag=dns json Question.Hdr.Name Question.A | require -v A | count by Name | table Name count
```

���̌����́ATCP���M���|�[�g�܂���UDP���M���|�[�g�̂����ꂩ���w�肳��Ă���p�P�b�g��ʉ߂��܂�:

```
tag=pcap packet tcp.SrcPort as tsp udp.SrcPort as usp | require tsp usp | table tsp usp
```

���̌����́AIPv4���M��IP �� TCP���M���|�[�g�̗����������Ȃ��p�P�b�g�����ׂăh���b�v���܂�:

```
tag=pcap packet tcp.SrcPort ipv4.SrcIP | require -s SrcPort SrcIP | table SrcPort SrcIP
```
