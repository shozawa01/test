## Src

�\�[�X���W���[���́A�\�[�X�Ɋ�Â��ăG���g�����t�B���^�����O���邽�߂Ɏg�p����܂��B  ����́A���ׂẴG���g���������j�o�[�T�����^�f�[�^���ڂł��B  ���̃��W���[���͓���̏ꏊ����o�Ă���G���g��������̂ɖ𗧂��܂��B  Src��IP�ƃT�u�l�b�g���t�B���^�����O�ł��܂��B

### �g�p��

����̃\�[�X����̃G���g�����폜���܂�:

```
tag=syslog,apache,pcap src != 192.168.1.1 | count by TAG | chart count by TAG
```

����̃T�u�l�b�g����̃G���g���݂̂�I�����܂�:

```
tag=syslog,apache,pcap src == 192.168.1.0/24 | count by SRC | chart count by SRC
```