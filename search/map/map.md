# Map modules

`pointmap`/`heatmap`�����_�����W���[���́A�}�b�v��Ɍ������ʂ������܂��B  �ǂ�����񋓒l�̈ʒu�Ɋ�Â��ă}�b�v�ɃG���g����z�u���܂��B  �f�t�H���g�ł́A���W���[����[geoip](#!search/geoip/geoip.md)�������W���[���ɂ���Đݒ肳�ꂽ `Location`�ƌĂ΂��񋓒l��T���܂��B  �ꏊ�́A�ȉ����g�p���Ė����I�Ɏw�肷�邱�Ƃ��ł��܂�:

* `-loc <enumerated value>`�́A�f�t�H���g��`Location`�ł͂Ȃ��A�w�肳�ꂽ�񋓒l�ŏꏊ��T���悤���W���[���Ɏw�����܂��B
* `-lat <enumerated value> -long <enumerated value>`�́A�ܓx�ƌo�x�̒l��ʁX�Ɍ�������悤���W���[���Ɏw�����܂��B  �����́A�i `geoip`���W���[���ɂ���Ē񋟂����j���������_���܂��͕ʂ̃\�[�X����̕�����ł�

�}�b�v�ɂ́A�ő�1000�|�C���g���\������܂��B����̓W�I�t�F���X�ł��B  �܂�A�}�b�v�̈ꕔ�ɃY�[���C������ƁA���̃G���A���ɍő�1000�|�C���g���\������܂��B

# Pointmap

�|�C���g�}�b�v�̓G���g�����}�b�v��̌ʂ̃}�[�J�[�ɕϊ����܂��B  �ǉ��̗񋓒l�����w�肳��Ă���ꍇ�́A�|�C���g���N���b�N���ꂽ�Ƃ��ɂ����̓��e���\������܂��B  

���̌����ł́Anetflow���R�[�h�ɋL�^����Ă��邷�ׂĂ�IP�A�h���X�̃}�b�v���\������܂�:

```
tag=netflow netflow IP | geoip IP.Location | pointmap IP
```

![](map1.png)

�eIP����̃o�C�g�������v���AIP�����Bytes�񋓒l���|�C���g�}�b�v�̈����ɒǉ�����ƁA�|�C���g���N���b�N����ƕ\������܂��i�b���Ă���WHO���m�F�ł���悤��ASN�g�D���ǉ����܂����j:

```
tag=netflow netflow IP Bytes | sum Bytes by IP | geoip IP.Location | geoip -r maxmindASN IP.ASNOrg | pointmap IP Bytes ASNOrg
```

![](map2.png)

# Heatmap

�q�[�g�}�b�v�̓|�C���g�}�b�v�Ɠ��l�ɋ@�\���܂����A�����Ƃ���0�܂���1�̒ǉ��̗񋓒l�����܂��B  �񋓒l�̈������^�����Ă��Ȃ��ꍇ�́A�e�ꏊ�̃G���g������`heat`�Ƃ��ăq�[�g�}�b�v�𐶐����܂��B  �l�b�g�t���[���R�[�h���g�p���邱�̗�ł́A`heat`�̓��P�[�V��������̐ڑ�����\���܂�:

```
tag=netflow netflow IP | geoip IP.Lat IP.Long | heatmap -lat Lat -long Long
```

![](map3.png)

���v�o�C�g���������Ƃ��Ēǉ�����ƁA`heat`�͐ڑ����ł͂Ȃ��A�ڑ�����đ��M���ꂽ�o�C�g�����瓱���o����܂�:

```
tag=netflow netflow IP Bytes | sum Bytes by IP | geoip IP.Location | heatmap sum
```

![](map4.png)

## 3D�}�b�v�\��

�q�[�g�}�b�v�ƃ|�C���g�}�b�v�ɂ�3D�����_�����O������܂��B  �}�b�v�̉E��ɂ���uGlobe�v�Z���N�^���N���b�N���邾���Ń}�b�v���ĕ`�悳��܂��B

![](selector.png)

�܂����������q�[�g�}�b�v�N�G�������s���܂����AGlobe�V�X�e�����g�p���ă����_�����O����ƁA���̂悤�ɂȂ�܂�:

![](map5.png)

�������A����1�̋C�̗������g���b�N������܂��B  ���ׂẴO���[�o���ȋ��Ђɂ��ă��A���^�C���Ŋm���ɍX�V����Ă��邱�Ƃ�m�点�邽�߂ɁA���[�e�[�V������ǉ��ł��܂��B

![](rotation.gif)
