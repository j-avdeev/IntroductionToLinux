9. Install vsftp-server
9.1 Install by apt-get
$ sudo apt-get install vsftpd

9.2 Check vsftpd working
$ ps aux | grep ftp

9.3 Check and connect to ftp. Type in Windows file explorer
ftp://192.168.0.102

where 192.168.0.102 - VM ip addres.
Check file permissions. Try to add folder, file. Delete folder.

9.4 Backup settings file
$ sudo cp /etc/vsftpd.conf /etc/vsftpd.conf.default

9.5 Edit settings file
$ sudo nano /etc/vsftpd.conf

9.6 Make following changes:

# run in standalone mode
listen=YES

# Anonimous access
no_anon_password=YES

# Anonim users will get to pub directory
anon_root=/var/ftp/pub
anon_umask=022

9.7* Add SSL encription
(http://bezopasnik.org/linux/dok/Debian/9.htm)

