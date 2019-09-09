## Anko

anko���W���[����eval�̕⑫�Ƃ��Ă�芮�S�ȃX�N���v�g����񋟂��܂��B�����G���g���ɑ΂��Ă�蕡�G�ȑ�����\�ɂ��܂����A�P����eval������anko�X�N���v�g�̊J���A�e�X�g�A����ѓW�J�ɑ����̍�Ƃ��K�v�ɂȂ�܂��B�X�N���v�g��[���\�[�X�V�X�e��](#!resources/resources.md)�̃��\�[�X�Ƃ��ĕۑ�����܂��B

anko�̍\����eval�̍\���Ɠ����ł��B�ǂ����[github.com/mattn/anko](https://github.com/mattn/anko)����h�����Ă���AGravwell�ŗL�̃^�X�N�p�ɂ������̒ǉ��@�\���ǉ�����Ă��܂��B

���̃��W���[�����\���ɋ@�\���Ȃ��󋵂ł�anko���g�p���邱�Ƃ������߂��܂��B�ʏ�A����́A�G���g�����ȑO�̃G���g���Ɣ�r����K�v������A�G���g���𕡐�����K�v������A�G���g������f�[�^�𒊏o����̂ɕ��G�ȑ��삪�K�v�ȁA�܂��͂����̑g�ݍ��킹�̏󋵂��Ӗ����܂��B

�h�L�������g�̂��̕����ł́Aanko���W���[���̎g�����ɂ��ĊȒP�ɐ������Ă��܂��B���ڍׂȐ����ɂ��ẮA[���S��anko���W���[���̃h�L�������g](#!scripting/anko.md)��[Anko�X�N���v�g����̃h�L�������g](#!scripting/scripting.md)���Q�Ƃ��Ă��������B

### �\��

`anko <script name> [script arguments]`

Anko�X�N���v�g�̓��\�[�X�Ƃ��ĕۑ�����Ă��܂��B���\�[�X�̖��O�́Aanko���W���[���ւ̍ŏ��̈����Ƃ��Ďw�肷��K�v������܂��B�X�N���v�g���̌�ɁA�ǉ��̈������X�N���v�g���̂ɓn����܂��B

### �X�N���v�g��

���̃X�N���v�g�́Aeval���W���[���̃h�L�������g�̗���ăt�H�[�}�b�g�������̂ł��B1�s��eval�̗�����͂邩�ɓǂ݂₷�����Ƃɒ��ӂ��Ă�������:

```
func Process() {
	if len(Body) <= 10 {
		setEnum("postlen", "short")
	} else if len(Body) > 10 && len(Body) < 300 {
		setEnum("postlen", "medium")
	} else {
		setEnum("postlen", "long")
	}
}
```

�X�N���v�g��`CheckPostLen`�Ƃ������O�̃��\�[�X�ɃA�b�v���[�h����Ă���Ɖ��肷��ƁA�X�N���v�g�͎��̂悤�Ɏ��s�ł��܂�:

```
tag=reddit json Body | anko CheckPostLen | count by postlen | table postlen count
```

����`Process`�֐��́Aanko���W���[���ɓ��B���錟���G���g�����Ƃ�1����s����A�񋓒l�̒������m�F���āA�{�̂̒����Ɋ�Â���`Body`�A�V�����񋓒l`postlen`��ݒ肵�܂��B

���̗�͂ƂĂ��ȒP�ł��B`Process`�֐��݂̂��������Ă��܂��i�I�v�V����`Parse`�܂���`Finalize`�֐��͎�������Ă��܂���j�B��蕡�G�ȗ�ɂ��ẮA[���S��anko���W���[���̃h�L�������g](#!scripting/anko.md)���Q�Ƃ��Ă��������B