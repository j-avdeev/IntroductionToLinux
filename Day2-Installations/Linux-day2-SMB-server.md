# Install smb-server
1. Install by apt-get

```
$ sudo apt-get install samba
```
2. Change /etc/samba/smb.conf file with help of smb.conf in github repo

3 Create share dir
```
$ sudo mkdir /var/smb
```

4. Allow read and write permissions
```
$ sudo chmod ugo+rwx /var/smb
```
5 Restart Samba
```
$ sudo service smbd restart
$ sudo service nmbd restart
```
6 Check and connect to samba-server. Type in Windows file explorer
```
//192.168.0.102
```
or for Linux
```
smb://192.168.0.102
```
where 192.168.0.102 - VM ip addres.

Check file permissions. Try to add folder, file. Delete folder.
