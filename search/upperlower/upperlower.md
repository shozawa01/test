## Upper / Lower

upper���W���[����lower���W���[���́A�e�L�X�g��啶���܂��͏������ɕϊ����܂��B  �P��`upper`�i�܂���`lower`�j���Ăяo���ƁA�G���g���̐��f�[�^���啶���ɕϊ�����܂��B  1�ȏ�̗񋓒l�̖��O�̃��X�g���g�p���ă��W���[�����Ăяo���ƁA�����̗񋓒l�͂��ׂđ啶���܂��͏������ɕϊ�����܂��B  �����`unique`�Ȃǂ̃��W���[���ɓn���O�Ƀf�[�^�𐳋K������̂ɖ𗧂��܂��B

### �g�p��

���̗�ł́A`upper`�J�E���g�O��Shodan�f�[�^�𐳋K�����邽�߂Ƀ��W���[�����g�p���Ă��܂��B

```
tag=shodan json location.region_code | upper region_code | count by region_code | table region_code count
```