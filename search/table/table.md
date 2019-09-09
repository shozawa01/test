# Table

�e�[�u�������_���[�̓e�[�u�����쐬���邽�߂Ɏg�p����܂��B  �e�[�u�����\�z����ɂ́A�e�[�u�������_���[�Ɉ�����n���܂��B  �����͗񋓒l�ATAG�ATIMESTAMP�A�܂���SRC�łȂ���΂Ȃ�܂���B  �����̓e�[�u���̗�Ƃ��Ďg�p����܂��B

��������w�肵�Ȃ��ƁAtable�͂��ׂĂ̗񋓒l���Ƃ��ĕ\�����܂��B  ����͒����ɖ𗧂��܂��B

## �T�|�[�g����Ă���I�v�V����

* `-save <destination>`: ���ʂ̃e�[�u����lookup���W���[���p�̃��\�[�X�Ƃ��ĕۑ����܂��B  ����́A���錟���̌��ʂ�ۑ����iDHCP���O����MAC����IP�ւ̃}�b�s���O�𒊏o����Ȃǁj�A��̌����Ŏg�p����̂ɕ֗��ȕ��@�ł��B
* `-csv`: -save�t���O�Ƒg�ݍ��킹�āA�l�C�e�B�u��Gravwell�`���ł͂Ȃ�CSV�`���Ńe�[�u����ۑ����܂��iCSV�̓��b�N�A�b�v���W���[���Ƃ��݊���������܂��j�B �f�[�^���G�N�X�|�[�g����Ƃ��ɕ֗��ł��B
* `-update <key>`: `-save`�t���O�Ƒg�ݍ��킹�āA�����̃e�[�u�����㏑������̂ł͂Ȃ��X�V���܂��B ����́A�X�P�W���[���������g�p���āA���Ƃ��� �l�b�g���[�N�ł���܂łɌ���ꂽ���ׂĂ�MAC�A�h���X�̃��X�g�B �����̃��b�N�A�b�v�e�[�u���̗�́A�����Ƃ��Ďw�肳�ꂽ��ƈ�v����K�v������܂��B "key"�I�v�V�����́A�����ꂩ�̗�̖��O�ł��B �Â����b�N�A�b�v�e�[�u���ƐV�������b�N�A�b�v�e�[�u�����}�[�W����Ƃ��A�Â��e�[�u���̍s�́A���̃L�[�t����̒l���V�����e�[�u���ɑ��݂��Ȃ��ꍇ�ɂ̂݊܂܂�܂��B
* `-nt`: �e�[�u����non-temporal���[�h�ɂ��܂��B ����ɂ��A�㗬�̐��w���W���[���́A�e�[�u���Ɏ��s������̂ł͂Ȃ��A���ʂ����k���܂��B ����ɂ��A�ꎞ�I�ȕ��I�����s�v�ȏꍇ�ɁA��ʂ̃f�[�^�̌�����啝�ɍ������ł��܂��B ���݁A[stats module](#!search/stats/stats.md)���g�p����ꍇ�ɂ��K�v�ł��B

## �T���v���N�G��

### ��{�e�[�u���p

Netflow���R�[�h���炢�����̗v�f�𒊏o���āA�e�[�u���ɂ����������I�ɕ\�������܂�:

```
tag=netflow netflow Src Dst SrcPort DstPort | table
```

�u���[�g�t�H�[�XSSH�U����������:

```
tag=syslog grep sshd | regex "authentication error for (?P<user>\S+)" | count by user | table user count
```

![](table-render.png)

### -nt�I�v�V�������g�p����

��ʂ̃f�[�^������󋵂ł́Acount���W���[��������Ɍ��ʂ����k����悤�ɁAtable��non-temporal���[�h�ɋ������܂�:

```
tag=jsonlogs json source | count by source | table -nt source count
```

### -save�I�v�V�������g�p����

DHCP���O���g�p���āAIP����MAC�ւ̃}�b�s���O���܂ރ��b�N�A�b�v�e�[�u�����쐬���܂�:

```
tag=syslog regex "DHCPACK on (?P<ip>\S+) to (?P<mac>\S+)" | unique ip mac | table -save ip2mac ip mac
```

�����āA���b�N�A�b�v�e�[�u�����g����SSH���O�C���Ɋ֘A����MAC�������܂�:

```
tag=syslog grep sshd | regex "Accepted .* for (?P<user>\S+) from (?P<ip>\S+)" | lookup -r ip2mac ip ip mac as mac |table user ip mac
```

![](table-ipmac.png)

### -update�I�v�V�������g�p����

���̗�ł́A���[�J���l�b�g���[�N�Ō�����IP�A�h���X���܂ރe�[�u�����쐬���A����ɍX�V���܂��B

�ŏ��ɁA192.168.2.0/24�l�b�g���[�N�Ō������ӂ̃v���C�x�[�gIPv4�A�h���X�����ׂĊ܂ރe�[�u�����쐬���܂��B

```
tag=pcap packet ipv4.SrcIP ~ PRIVATE | unique SrcIP | subnet SrcIP /24 | eval subnet == toIP("192.168.2.0") | table -save test -csv SrcIP
```

![](update1.png)

���ʂ̃��\�[�X�i'test'�Ƃ������O�j���_�E�����[�h����ƁA�\�z�����e�[�u�����\������܂��B:

```
SrcIP
192.168.2.1
192.168.2.52
192.168.2.60
192.168.2.51
192.168.2.61
```

���ɁA192.168.0.0/24�T�u�l�b�g�Ō�����IP��*�ǉ�*���邽�߂ɕʂ̌��������s���܂�:

```
tag=pcap packet ipv4.SrcIP ~ PRIVATE | unique SrcIP | subnet SrcIP /24 | eval subnet == toIP("192.168.0.0") | table -update SrcIP -save test -csv SrcIP
```

![](update2.png)

*�\��*����Ă���e�[�u���ɂ͐V����IP�A�h���X�݂̂��\������Ă��܂����A���\�[�X�ɂ͗����̌������ʂ��܂܂�Ă��܂�:

```
SrcIP
192.168.0.50
192.168.0.60
192.168.0.1
192.168.0.71
192.168.0.30
192.168.0.2
192.168.0.73
192.168.0.70
192.168.0.42
192.168.0.72
192.168.2.1
192.168.2.52
192.168.2.60
192.168.2.51
192.168.2.61
```

update�̈����Ƃ���'SrcIP'��n���܂����B����͏d���r���Ɏg�p����܂��B SrcIP���V�����e�[�u���̍s�ƈ�v����Â��e�[�u���̍s�́A�X�V���ꂽ���\�[�X�Ɋ܂܂�܂���B
