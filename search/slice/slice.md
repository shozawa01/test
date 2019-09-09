## Slice

�X���C�X���W���[���́A�G���g��/�񋓒l���̃I�t�Z�b�g���w�肵�A�I�v�V�����ł����̃o�C�g�����̌^�ɃL���X�g���邱�ƂŁA�G���g���܂��͗񋓒l����o�C�g�𒊏o���邽�߂̋��͂Ŕ��ɒ჌�x���̃c�[���ł��B  �X���C�X�́A���̐����܂ޑ��΃C���f�b�N�X����ăo�C�g���Q�Ƃł��܂��B

���̌����ł́A "data"�񋓒l�̍ŏ���2�o�C�g��ǂݎ��A�����16�r�b�g�r�b�O�G���f�B�A�������Ƃ��ĉ�͂��邱�Ƃɂ���āA�g���^�Ԃ̃L�����o�X���b�Z�[�W����RPM�𒊏o���܂��B

```
tag=CAN canbus ID=0x2C4 | slice uint16be(data[0:2]) as RPM | mean RPM | chart mean
```

�X���C�X�͐��̃G���g���̓��e���璊�o���邱�Ƃ��A�񋓒l�𑀍삷�邱�Ƃ��ł��܂��B  ���o���ꂽ�o�C�g�́A�����╶����ȂǁA�I�v�V�����ŕʂ̌^�ɉ�͂ł��܂��B  �������̗�:

| �R�}���h | ���� |
|---------|-------------|
| `slice [0:4] as foo` | �G���g���̃f�[�^����ŏ���5�o�C�g�𒼐ڒ��o���A�񋓒l"foo"�ɔz�u���܂� |
| `slice Payload[9] as tenth` |  �񋓒l"Payload"����10�o�C�g�ڂ𒊏o���܂� |
| `slice uint16le(Payload[9:10]) as value` | �񋓒l"Payload"����2�o�C�g�������o���A�����Ȃ�16�r�b�g���g���G���f�B�A���Ƃ��ĉ�͂��A"value"�Ƃ��ĕۑ����܂��B |
| `slice uint16be(Payload[-2:]) as value` | "Payload"����Ō��2�o�C�g�����o���A�����Ȃ�16�r�b�g�r�b�O�G���f�B�A�������Ƃ��ĉ�͂��A"value"�Ƃ��ĕۑ����܂��B |
| `slice uint16be(Payload[-4:-2]) as value2` | "Payload"�̍Ō��2�o�C�g�ɐ�s����2�o�C�g���v�����A�����𕄍��Ȃ�16�r�b�g�r�b�O�G���f�B�A�������Ƃ��ĉ�͂��A"value2"�Ƃ��Ċi�[���܂��B

### �T�|�[�g����Ă���^

�X���C�X���W���[���̕s���ȋ@�\�́A�f�[�^��K�؂Ȍ^�ɃL���X�g���邱�Ƃł��B  �f�t�H���g�ł́A�f�[�^�̓o�C�g�X���C�X�Ƃ��Ē��o����܂����A�I�v�V����cast���g�p����ƁA�f�[�^���^�ɕϊ��ł��܂��B  �ube�v�̐ڔ��������^��[�r�b�O�G���f�B�A��](https://en.wikipedia.org/wiki/Endianness)�̃r�b�g���������A�ube�v�ڔ����̂Ȃ����̂̓��g���G���f�B�A���̃r�b�g�����g�p���܂��B


* byte
* int16
* int16le
* int16be
* uint16
* uint16le
* uint16be
* int32
* int32le
* int32be
* uint32
* uint32le
* uint32be
* int64
* int64le
* int64be
* uint64
* uint64le
* uint64be
* float32
* float32le
* float32be
* float64
* float64le
* float64be
* array
* string

### �C�����C���t�B���^�����O

�X���C�X���W���[���́A�o�C�i���f�[�^�̔��ɍ����ȏ������\�ɂ���C�����C���t�B���^�����O���T�|�[�g���܂��B  ���ׂẴ^�C�v�����ׂẴt�B���^������T�|�[�g����킯�ł͂���܂���B  ���Ƃ��΁A���������_������T�u�Z�b�g�������悤�Ƃ��Ă��Ӗ����Ȃ��A�o�C�g�X���C�X�Ɂu���Ȃ�v��K�p���Ă��Ӗ�������܂���B  �ȉ��́A�t�B���^���Z�q�̊��S�ȃ��X�g�ƁA�ǂ̉��Z�q���ǂ̃^�C�v�ɓK�p�ł��邩�������\�ł�:

#### �t�B���^���Z�q

| �I�y���[�^�[ | �� | ����
|----------|------|-------------
| == | ������ | �t�B�[���h�͓������Ȃ���΂Ȃ�܂���
| != | �������Ȃ� | �t�B�[���h�͓������Ă͂����܂���
| < | ���� | �t�B�[���h�͂�菬����
| > | ���傫�� | �t�B�[���h�͂��傫���Ȃ���΂Ȃ�܂���
| <= | �ȉ� | �t�B�[���h�͈ȉ��łȂ���΂Ȃ�܂���
| >= | �ȏ� | �t�B�[���h�͈ȏ�łȂ���΂Ȃ�܂���
| ~ | �T�u�Z�b�g | �t�B�[���h�̓����o�[�łȂ���΂Ȃ�܂���
| !~ | �T�u�Z�b�g�ł͂Ȃ� | �t�B�[���h�̓����o�[�ł����Ă͂����܂���

#### �^�C�v�ʃT�|�[�g���Z�q

Type     | == | != | ~ | !~ | < | <= | > | >=
----------|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:
byte     | X | X |  |  | X | X | X | X 
int16    | X | X |  |  | X | X | X | X
int16le  | X | X |  |  | X | X | X | X
int16be  | X | X |  |  | X | X | X | X
uint16   | X | X |  |  | X | X | X | X
uint16le | X | X |  |  | X | X | X | X
uint16be | X | X |  |  | X | X | X | X 
int32    | X | X |  |  | X | X | X | X
int32le  | X | X |  |  | X | X | X | X
int32be  | X | X |  |  | X | X | X | X
uint32   | X | X |  |  | X | X | X | X
uint32le | X | X |  |  | X | X | X | X
uint32be | X | X |  |  | X | X | X | X
int64    | X | X |  |  | X | X | X | X
int64le  | X | X |  |  | X | X | X | X
int64be  | X | X |  |  | X | X | X | X
uint64   | X | X |  |  | X | X | X | X
uint64le | X | X |  |  | X | X | X | X
uint64be | X | X |  |  | X | X | X | X
float32  | X | X |  |  | X | X | X | X
float32le| X | X |  |  | X | X | X | X
float32be| X | X |  |  | X | X | X | X
float64  | X | X |  |  | X | X | X | X
float64le| X | X |  |  | X | X | X | X
float64be| X | X |  |  | X | X | X | X
array    | X | X | X | X |  |  |  |
string   | X | X | X | X |  |  |  |

