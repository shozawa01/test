## Hexlify

hexlify���W���[���́A�f�[�^��ASCII��16�i�\���ɃG���R�[�h���邽�߂Ɏg�p����܂��B  ���̃��W���[���́A���m�̃f�[�^�^�Ɏ��g�݁A�o�C�i���f�[�^������������@���w�ԂƂ��ɖ𗧂��܂��B  ���Ƃ��΁Acanbus�f�[�^���璊�o���ꂽ���m�̗񋓒l���G���R�[�h���邱�Ƃ�����܂��B  �قƂ�ǂ̐�������canbus�̎d�l�����J���Ă��܂��񂪁AID���璊�o����16�i���ŃG���R�[�h���邱�ƂŁA�\���\�ȃp�^�[���ŕω����Ă���l�����ʂ��A�p�����[�^�����ʂ���̂ɖ𗧂��܂��B  ����́AGravwell�`�[�����AFiat Chrysler of America��canbus ID�ɃA�N�Z�X�����ɁARAM 1500�g���b�N�̃K�X���x���A���x�A����уX���b�g���ʒu��PDU�𓱂��o�������@�ł��B

### �T�|�[�g����Ă���I�v�V����

* `-d`: int��ASCII 16�i���Ƃ��ăG���R�[�h����̂ł͂Ȃ��AASCII 16�i���𐮐��Ƀf�R�[�h���܂��B


### ���ׂẴf�[�^��16�i�����邽�߂̌�����

```
tag=stuff hexlify
```

### 1�̗񋓒l��16�i���ɂ��邽�߂̌�����

```
tag=CAN canbus ID Data | hexlify Data | table ID Data
```

### ���ׂẴf�[�^��16�i���ɂ��ĐV�������O�Ɋ��蓖�Ă邽�߂̌�����

```
tag=stuff hexlify DATA as hexdata | table DATA hexdata
```

### �������̗񋓒l���Ċ��蓖�Ă�16�i�������邽�߂̌�����

```
tag=CAN canbus ID Data | hexlify ID as hexid Data as hexdata | table ID hexid DATA hexdata
```

### 16�i�f�[�^�̃f�R�[�h��

```
tag=apache json val | hexlify -d val as decodedval | table val decodedval
```
