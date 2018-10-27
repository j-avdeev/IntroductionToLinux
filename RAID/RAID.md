Что такое и разновидности RAID:
https://ru.wikipedia.org/wiki/RAID

1. Создание RAID1 из 2 виртуальных жестких дисков
Что-то наподобие такого:
http://blog.102web.ru/howto/debian-mdadm/


2. Добавить e-mail уведомления о статусе RAID.
Что-то наподобие такого:
https://dustymabe.com/2012/01/29/monitor-raid-arrays-and-get-e-mail-alerts-using-mdadm/


1. Добавляем в виртуальную машину еще один виртуальный жесткий диск
2. Убеждаемся, что у нас теперь два жестких диска
$ fdisk -l
3. apt-get install mdadm
4. Скопировать таблицу разделов со старого диска на новый
$ dd if=/dev/sda of=/dev/sdb bs=512 count=1
5. Меняем идетификатор раздела на новом (sdb) с 83 (стандартный раздел Linux) на fd (Linux raid autodetect)

# fdisk /dev/sdb
Command (m for help): t
Selected partition 1
Hex code (type L to list codes): fd
Changed system type of partition 1 to fd (Linux raid autodetect)
Command (m for help): w

6. Создаем разделы
# mdadm --create /dev/md0 --level=1 --raid-disks=2 missing /dev/sdb1
# mdadm --create /dev/md1 --level=1 --raid-disks=2 missing /dev/sdb2

7. Проверяем

$ cat /proc/mdstat
