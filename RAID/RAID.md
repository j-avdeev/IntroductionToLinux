Что такое и разновидности RAID:
https://ru.wikipedia.org/wiki/RAID

1. Создание RAID1 из 2 виртуальных жестких дисков
Что-то наподобие такого:
http://blog.102web.ru/howto/debian-mdadm/

SoftwareRaid: 1 HDD с системой, 2х HDD под RAID1.
https://wiki.debian.org/SoftwareRAID

`# fdisk /dev/sdb`
n p 1 . . q

`# fdisk /dev/sdc`
n p 1 . . q




2. Добавить e-mail уведомления о статусе RAID.
Что-то наподобие такого:
https://dustymabe.com/2012/01/29/monitor-raid-arrays-and-get-e-mail-alerts-using-mdadm/

***

1. Добавляем в виртуальную машину еще один виртуальный жесткий диск
2. Убеждаемся, что у нас теперь два жестких диска

`$ fdisk -l`

3. `# apt-get install mdadm`
4. Скопировать таблицу разделов со старого диска на новый

`$ dd if=/dev/sda of=/dev/sdb bs=512 count=1`

5. Меняем идетификатор раздела на новом (sdb) с 83 (стандартный раздел Linux) на fd (Linux raid autodetect)

`# fdisk /dev/sdb`

Command (m for help): t

Selected partition 1

Hex code (type L to list codes): fd

Changed system type of partition 1 to fd (Linux raid autodetect)

Command (m for help): w

6. Создаем разделы

`# mdadm --create /dev/md0 --level=1 --raid-disks=2 missing /dev/sdb1`

`# mdadm --create /dev/md1 --level=1 --raid-disks=2 missing /dev/sdb2`

7. Проверяем

`$ cat /proc/mdstat`

`# mkfs.ext4 /dev/md126` (bigger)

`# mkswap /dev/md127` (smaller)


`# cp /etc/mdadm/mdadm.conf /etc/mdadm/mdadm.conf.backup`

`# mdadm --examine --scan >> /etc/mdadm/mdadm.conf`

8. Монтируем рейд в папку /mnt

`# mount /dev/md126 /mnt`

9. Копируем все от / и ниже в /mnt

`# cp -dpRx / /mnt`

10. Открываем файл настроек монтирования разделов

`# nano /mnt/etc/fstab`

`/dev/md126 /               ext4    errors=remount-ro 0       1`
`# swap was on /dev/vda5 during installation`
`/dev/md127 none            swap    sw              0       0`

вместо /dev/md126, /dev/md127 писать UUID, которые можно посмотреть командой blkid

11. Устанавливаем и конфигурируем grub

`grub-install --root-directory=/mnt/ /dev/sdb`

`grub-install --recheck /dev/sdb`

12. `# nano /mnt/etc/default/grub`

Раскомментировать
`GRUB_TERMINAL=console`

`mount --bind /dev /mnt/dev`

`mount --bind /sys /mnt/sys`

`mount --bind /proc /mnt/proc`

`chroot /mnt`

`update-grub`

13. Смотрим `# nano /boot/grub/grub.cfg`

14. Проверяем UUID

`# blkid`

15. Перезагружаемся
`# exit`
`# shutdown -r now`

16. Снова подключаемся по ssh

`# ssh vagrant@10.101.6.44`



md0 127 8.9 GB 126

md1 126 1021.4 MB 127
