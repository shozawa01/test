# Alias

alias���W���[���́A�����̗񋓒l�ɒǉ��̖��O�����蓖�Ă邱�Ƃ��ł��܂��B �V�����񋓒l��ύX���Ă��A���̒l�͕ς��܂���B����́A���b�N�A�b�v���W���[���p�ɒ��o���ꂽ�񋓒l�����O�ɐݒ肵�����ꍇ�ɓ��ɕ֗��ł�:

```
tag=pcap packet ipv4.SrcIP | ip SrcIP ~ PRIVATE | alias SrcIP src_host | lookup -r hosts SrcIP ip hostname as src_host | count by src_host | table src_host SrcIP count
```

![](alias.png)

alias���W���[���́Asource��destination��2�̈��������܂��B ���������āA��L�̗�ł́A�����̗񋓂��ꂽ 'SrcIP'�� 'src_host'�ɃG�C���A�X����Ă��܂��B �������W���[�������̌��ʂ� 'src_host'�񋓒l�ɏ����o���Ă��A���� 'SrcIP'�l�͕ύX����܂���B