# Stackgraph

�X�^�b�N�O���t�����_���́A�ςݏd�˂�ꂽ�f�[�^�|�C���g���������_�O���t��\�����邽�߂Ɏg�p����܂��B  �X�^�b�N�O���t�́A��A�̃^�O�ɂ킽���ĕ����̃R���|�[�l���g����ݐς��ꂽ���ʂ̑傫����\������̂ɖ𗧂��܂��B  stackgraph�����_���[�̓A�L�������[�^�ł��B  �܂�A�㗬�̌������W���[���̓�������߂��A�T�u�Z���N�V�����Ɋ�Â��Č��ʂ��Čv�Z���邱�Ƃ��ł��܂��B  Gravwell�̗p��ł́Astackgraph��2�������ƑI�����T�|�[�g���Ă��܂��B

Stackgraph�̌Ăяo���ɂ�3�̈������K�v�ł��B  ����͏㗬�̌����R���|�[�l���g�ɂ���Ē��o���ꂽ�񋓒l�̖��O�łȂ���΂Ȃ�܂���B  ����1�́AIP�A�h���X�ȂǁA�X�̐����o�[�ɖ��O��t����񋓒l���w�肵�܂��B  ����2�́A�Ⴆ��TCP�|�[�g�̂悤�ɁA�e�����o�[�̌X�̗v�f��^����񋓒l���w�肵�܂��B  ����3�́A�����o�[���̊e�X�^�b�N�l�̑傫���̐�����\���傫���̒l�ł��B  �}�O�j�`���[�h�����̗�́Acount�Asum�Astddev�Asum�Amax�Amin�ł��B  �����̋c�_�𗝉�����ł��ȒP�ȕ��@�́A�ȉ��̗�𒲂ׂ邱�Ƃł��B

���F�f�[�^��stackgraph�ɑ��M����O�Ƀ\�[�g���Ă��A�]�݂ǂ���̂��Ƃ͂ł��܂���B  ���Ȃ���IP->�|�[�g�̃y�A�̐��������Ă��āA���̐��Ɋ�Â��ă\�[�g���Ă���X�^�b�N�O���t�i�Ⴆ��count by SrcIP,DstPort | sort by count desc | table SrcIP DstPort count�j�ɑ��邱�Ƃɋ���������Ȃ�A���X�g�̍ŏ��̍��ڂ͔��ɍ������������Ă��܂���1�݂̂̃|�[�gIP ���Ƃ��΁A�|�[�gIP 10.0.0.1���J�E���g10000�̃|�[�g443�ŁA����8�̃G���g����8�̈قȂ�IP�ŁA���ׂ�9000�͈̔͂̃|�[�g80���g�p���Ă���Ƃ���ƁA�|�[�g443�̓O���t��ŏ������Ȃ�܂��B

## ��

�X�^�b�N�O���t���L�q����őP�̕��@�́A�J�b�v����\�����邱�Ƃł��B  


### IP����у|�[�g�ʂ̃g���t�B�b�N��

```
tag=netflow netflow Src ~ PRIVATE Port < 1024 Bytes as traffic |  sum traffic by Src,Port | stackgraph Src Port sum
```

![IP Port Traffic Volumes](IPPortTraffic.png)

### Port����э��ɂ��ʐM��

```
tag=netflow netflow Src ~ PRIVATE Dst  Bytes as traffic Port |  geoip Dst.CountryName | sum traffic by Port, CountryName | stackgraph CountryName Port sum
```

![Country Traffic by Port](CountryPortTraffic.png)

### ���ʂ���ю��s���[�U�[�ʂ�SSH���O�C�����s

```
tag=syslog grep sshd | regex "Failed password for (?P<user>\S+) from (?P<ip>\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}) " | geoip ip.Country | count by user,Country | stackgraph Country user count
```

![Failed SSH Logins by Country](SSHUserCountry.png)

### ���ʂ���ю��s���[�U�[�ʂ�SSH���O�C�����s�i�����폜�j

```
tag=syslog grep sshd | regex "Failed password for (?P<user>\S+) from (?P<ip>\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}) " | geoip ip.Country != CN | count by user,Country | stackgraph Country user count
```

![Failed SSH Logins by Country Without China](SSHUserCountryNoChina.png)
