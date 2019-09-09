## Lookup

Lookup���W���[���́A���\�[�X�Ɋi�[����Ă���ÓI�f�[�^�\�[�X����f�[�^�̏[���ƕϊ����s�����߂Ɏg�p����܂��B

```
lookup -r <resource name> <enumerated value> <column to match> <column to extract> as <valuename>
```

���F�\���� ```as <valuename>```�̒ǉ���񋟂��Ȃ��ꍇ�A���b�N�A�b�v�͗񋓒l�����b�N�A�b�v���璊�o�����l�ɒu�������܂��B

�ǉ��̑�����܂Ƃ߂ĕ����񉻂��邱�ƂŁAlookup���W���[����1��̌Ăяo���ŕ�����lookup������w��ł��܂��B

### �T�|�[�g����Ă���I�v�V����
* `-r <arg>`: "-r"�I�v�V�����́A�ǂ̌������\�[�X���g�p���ăf�[�^���[�������邩���������W���[���ɒʒm���܂��B
* `-s`: "-s"�I�v�V�����́A�������W���[�����A�w�肳�ꂽ���ׂĂ̑��삪�������邱�Ƃ�v�����邱�Ƃ��w�肵�܂��B
* `-v`: "-v"�t���O�́A���b�N�A�b�v���W���[�����̐��䃍�W�b�N�𔽓]���܂��B  �܂�A����������v�͗}������A��v���Ȃ�������v�͓n����܂��B  "-v"�� "-s"�t���O��g�ݍ��킹�Ċ�{�I�ȃz���C�g���X�g���쐬���A�w�肳�ꂽ���b�N�A�b�v�e�[�u���ɑ��݂��Ȃ��l�݂̂�n�����Ƃ��ł��܂��B

### lookupdata���\�[�X��ݒ肷��

���b�N�A�b�v�f�[�^�́A�݊����̂��郌���_�����O���W���[���i�Ⴆ�΁A�e�[�u�����W���[���j����_�E�����[�h����A�_�E�����[�h����ы��L����ї��p�̂��߂Ƀ��\�[�X�Ɋi�[���꓾��B  �������ʃy�[�W�̃��j���[���g�p���āA "LOOKUPDATA"��I�����Ă��̃t�H�[�}�b�g�̌������ʂ̕\���_�E�����[�h���邱�Ƃ�I���ł��܂��B

![Lookup Download](lookup-download.png)

[�e�[�u�������_��](#!search/table/table.md)�ɂ� `-save`�I�v�V�������p�ӂ���Ă���A��Ō����Ŏg�p���邽�߂Ɍ������ʃe�[�u�������\�[�X�Ƃ��Ď����I�ɕۑ����܂�:

```
tag=syslog regex "DHCPACK on (?P<ip>\S+) to (?P<mac>\S+)" | unique ip mac | table -save ip2mac ip mac
```

��L�̗�ł́A�e�[�u�������_����DHCP���O����h������MAC�A�h���X�ւ�IP�A�h���X�̃}�b�s���O���܂� `ip2mac`�Ƃ������O�̃��\�[�X�������I�ɍ쐬���܂�

#### CSV

CSV�f�[�^�����b�N�A�b�v���W���[���Ɏg�p�ł��܂��B  Gravwell�����������W���[����csv�t�@�C�������\�[�X�Ƃ��Ďg�p����ɂ́ACSV�ɗ�̈�ӂ̃w�b�_�[���܂܂�Ă���K�v������܂��B

### ������

���̗�ł́A����csv����쐬���ꂽ "macresolution"�Ƃ������\�[�X���g�p���܂�:
```
mac,hostname
mobile-device-1,40:b0:fa:d7:af:01
desktop-1,64:bc:0c:87:bc:71
mobile-device-2,40:b0:fa:d7:ae:02
desktop-2,64:bc:0c:87:9a:11
```

���ꂩ��A�p�P�b�g�f�[�^�̌����𔭍s���Alookup���W���[�����g�p���ăf�[�^�X�g���[�����������A�z�X�g�����܂߂܂��B  ���̏ꍇ�A�z�X�g���� "devicename"�񋓒l�Ɋ��蓖�Ă��܂��B

```
tag=pcap packet eth.SrcMAC | count by SrcMAC | lookup -r macresolution SrcMAC mac hostname as devicename |  table SrcMAC devicename count
```

����ɂ��A���̋������ꂽ�f�[�^���܂ރe�[�u�����쐬����܂�
```
64:bc:0c:87:bc:71	|	desktop-1       	|	52183
40:b0:fa:d7:ae:02	|	mobile-device-2 	|	21278
64:bc:0c:87:9a:11	|	desktop-2       	|	 2901
40:b0:fa:d7:af:01	|	mobile-device-1 	|	  927
```

#### ���b�N�A�b�v�e�[�u�����g�p�����z���C�g���X�g����̗�
```
tag=pcap packet eth.SrcMAC | count by SrcMAC | lookup -v -s -r macresolution SrcMAC mac hostname |  table SrcMAC count
```

����ɂ��A���b�N�A�b�v���X�g�Ɋ܂܂�Ă��Ȃ��������ׂĂ�MAC�A�h���X���܂ރe�[�u���������܂��B  �V�X�e���Ǘ��҂́A " - v"�� " - "�t���O���g�p���āA�l�b�g���[�N��̐V�����f�o�C�X�܂��̓C�x���g�X�g���[�����̐V�������O�̊�{�I�ȃz���C�g���X�g�Ǝ��ʂ�񋟂ł��܂��B
```
64:bc:0c:87:bc:60	|	24382
40:b0:fa:d7:ae:13	|	93485
64:bc:0c:87:9a:02	|	11239
40:b0:fa:d7:af:fe	|	   21
```
