## Canbus

canbus���W���[����CAN���b�Z�[�W����t�B�[���h�𒊏o���܂��i���Ȃ킿�ԗ��f�[�^�j�B �����̃t�B�[���h�́Acanbus���W���[���̌Ăяo���Ŏ����I�ɒ��o����܂��B

| mod | �t�B�[���h | �I�y���[�^ | ��
|-----|-------|-----------|----------
| canbus | ID | == != < > <= >= | canbus ID==0x341
| canbus | EID | == != < > <= >= | canbus EID==0x123456
| canbus | RTR | == != | canbus RTR==true
| canbus | Data | ~ !~ | canbus Data

### ������

���̌����ł́Acanbus�p�P�b�gID�ŃJ�E���g���A�ł��p�x�̍���ID���܂ޕ\��\�����܂��B

```
tag=vehicles canbus | count by ID | sort by count desc | table ID count
```

���̌����ł́A�X���b�g���f�[�^���w�肵�Ă���p�P�b�g�𒊏o���A�X���b�g���̕��ψʒu���v���b�g���܂��B
```
tag=vehicles canbus ID==0x123 Data | slice uint16be(Data[2:4]) as throttle | mean throttle | chart mean
```
