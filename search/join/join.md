# Join

�������W���[�����g�p����ƁA2�ȏ�̗񋓒l��P��̗񋓒l�Ɍ�������̂��ȒP�ɂȂ�܂��B  �o�C�g�X���C�X�ɂ̂݌����ł���o�C�g�X���C�X�������A�񋓌^�̒l�͂��ׂĕ�����ɕϊ�����ĘA������܂��B  �o�C�g�X���C�X�͎c��܂��B

���̌����ł́Anetflow���R�[�h���父��IP�ƃ|�[�g�𒊏o���A��������؂蕶���Ƃ��ăZ�~�R�����Ō������āA���ʂ�`dialstring`�Ƃ������O�̗񋓒l�ɔz�u���܂�:

```
tag=netflow netflow Dst DstPort | join -s : -t dialstring Dst DstPort | table Dst DstPort dialstring
```

�񋓒l�͂����ł��w��ł��܂��B  `-t`�t���O�́A�u�W�I�v�̗񋓒l���w�肵�܂��B  �w�肵�Ȃ��ꍇ�́A�ŏ��Ƀ��X�g���ꂽ�񋓒l���㏑������܂��B

## �T�|�[�g����Ă���I�v�V����

* `-s <separator>`:���ʂ̕�������̊e�񋓒l�̒l�̊ԂɁA�w�肳�ꂽ��؂蕶�����z�u���Ă��������B  �w�肵�Ȃ��ꍇ�A��؂蕶���͎g�p����܂���B  �o�C�g�X���C�X�ł͖�������܂��B
* `-t <target>`: �ŏ��̗񋓒l���㏑������̂ł͂Ȃ��A�w�肳�ꂽ���O�̗񋓒l�Ɍ��ʂ��i�[���Ă��������B

## ��

```
tag=pcap packet ipv4.SrcIP ~ 192.168.0.0/16 tcp.SrcPort | join -s : -t dialstring SrcIP SrcPort | unique SrcIP,SrcPort | table SrcIP SrcPort dialstring
```
![](join.png)
