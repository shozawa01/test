# Force Directed Graph

�L���O���t�ifdg�j���W���[���́A�m�[�h�y�A�ƃI�v�V�����̃O���[�v�����g�p���ėL���O���t�𐶐����邽�߂Ɏg�p����܂��Bfdg���W���[���́A���ʂƂ��ē�����G�b�W�̏d�ݒl�ƂƂ��ɁA���M���Ƒ��M��̃O���[�v���󂯓���܂��B

## �T�|�[�g����Ă���I�v�V����
* `-b`:�G�b�W���o�����ł��邱�Ƃ������܂��B�܂�A[A�AB]�̃y�A��[B�AA]�Ɠ����ł��B
* `-v <enumerated value>`: �G�b�W�͎w�肳�ꂽ�񋓒l�̍��v�Ƃ��ďd�ݕt�������ׂ��ł��邱�Ƃ������܂��B����-v�t���O�́A�G�b�W�����J�E���g�ȊO�̂��̂ŕ\�����d�݂����L���O���t�𐶐�����̂ɖ𗧂��܂��B
* `-sg <enumerated value>`: �O���t�̐F�t���Ɏg�p�����\�[�X�l�ɓK�p����O���[�v��񋟂��܂��B�Ⴆ�΁A�\�[�X�O���[�v�́A�O���t���̃m�[�h���O���[�v�����邱�Ƃ��\�ɂ���h�o�̂��߂̃T�u�l�b�g�ł��蓾�܂��B
* `-dg <enumerated value>`:-sg�Ɠ����ł����Adestination�p�����[�^�Ɋ�Â��ăO���[�v������Ă��܂��B

## �T���v���N�G��

�͗L���O���t���L�p�ł���Əؖ��ł�����́A�l�b�g���[�N��̃A�h���X�Ԃ̊֌W�����ʂ��邱�Ƃł��B�m�[�h���N���XC�l�b�g���[�N�ɃO���[�v�����Ȃ���IPV4�g���t�B�b�N�̏d�ݕt�������L���O���t�𐶐�����ɂ́A���̃N�G�����g�p���܂��B:

```
tag=pcap packet ipv4.SrcIP ipv4.DstIP ipv4.Length | sum Length by SrcIP,DstIP | subnet SrcIP /24 as SrcSub | subnet DstIP /24 as DstSub | fdg -v sum -sg SrcSub -dg DstSub SrcIP DstIP
```

![](fdg1.png)

�m�[�h�̏�Ƀ}�E�X��u���ƁA���̃��x���Ƃ��ׂ̗̃��x�����\������܂�:

![](fdg2.png)

�I�v�V�������j���[�ł́A�A�j���[�V������L���܂��͖����ɂ�����A�W���̋����L���O���t�Ɖ~�O���t��؂�ւ�����ł��܂�:

![](fdg3.png)
