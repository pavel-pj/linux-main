# linux-main

# DAY 3 : Users

#### check ussers

```bash
sudo cat /etc/passwd
```
#### check users and passwords hash 

```bash
sudo cat /etc/shadow
```
#### check group
```bash
sudo cat /etc/group
```
#### create user
```bash
sudo useradd -m -s /bin/bash junior_admin
```

#### add to group
```bash
sudo usermod -aG sudo junior_admin
```

#### add to group
```bash
sudo deluser junior_admin sudo
```

#### delete user :
```bash
 sudo deluser junior
```

#### delete group :
```bash
 sudo groupdel junior_admins
```

# DAY 4 : File System
## Создание отказоустойивого хранилища

### Raid

#### create Raid
```bash
sudo mdadm --create /dev/md0 --level=1 --raid-devices=2 /dev/sdb /dev/sdc
```
#### check :
```bash
sudo cat /proc/mdstat
```

#### create file system :
```bash
sudo mkfs.ext4 /dev/md0 
```
#### Mount to derictory
```bash
sudo mount /dev/md0 /mnt
```
####  create a file to check
```bash
sudo echo "Hello world" > /mnt/newfile
cat /mnt/newfile
```
#### fail one disk
```bash
sudo mdadm --fail /dev/md0 /dev/sdc
```
#### check:
```bash
sudo cat /proc/mdstat
```

#### check everything is ready to read
```bash
cat /mnt/newfile
```

#### delete
```bash
sudo umount /dev/md0
sudo mdadm --stop /dev/md0
sudo mdadm --zero-superblock /dev/sdc /dev/sdb
```


# LVM
## Разбивка диска на директории

#### create a physical device
```bash
sudo pvcreate /dev/sdb /dev/sdc
```
#### show a physical device
```bash
sudo pvdisplay
```
#### create a group
```bash
sudo vgcreate data_vg /dev/sdb /dev/sdc
```

#### show group
```bash
sudo vgdisplay 
```

#### create logical volume 1
```bash
sudo lvcreate -L 1G -n files_lv data_vg
```
#### create logical volume 2
```bash
sudo lvcreate -L 6G -n data_lv data_vg
```

#### make file system  1 :
```bash
sudo mkfs.ext4 /dev/data_vg/files_lv
```
#### make file system 2 :
```bash
sudo mkfs.ext4 /dev/data_vg/data_lv
```

####  mount 
```bash
sudo mount /dev/data_vg_/files_lv /mnt
```

####  mount 
```bash
sudo mount /dev/data_vg_/data_lv /backup
```

#### increase volume
#### from this output get a path to the next command :

```bash
df -h
```
```bash
sudo lvextend -L +1G  /dev/mapper/data_vg-files_lv
```
#### there is on increase in files_lv
```bash
df -h 
```

#### change file system
```bash
sudo resize2fs /dev/data_vg/files_lv
```

####  check
df -h
 
####  decrease other disk :

```bash
sudo umount /backup
sudo e2fsck -f /dev/mapper/data_vg-data_lv
sudo resize2fs /dev/mapper/data_vg-data_lv 4G
sudo lvreduce -L 4G /dev/mapper/data_vg-data_lv 
```

#### Adding 2 GB to the first volume
```bash
sudo lvextend -L +2G  /dev/mapper/data_vg-files_lv
sudo resize2fs /dev/data_vg/files_lv
df -h 
```
 
####  deactivate logical volume
```bash
sudo umount /mnt
sudo lvchange -an /dev/data_vg/files_lv
sudo lvremove /dev/data_vg/files_lv
```
####  the same for data_lv
```bash
sudo umount /backup
sudo lvchange -an /dev/data_vg/data_lv
sudo lvremove /dev/data_vg/data_lv
```

####  remove volume group and phisical volumes
```bash
sudo vgremove data_vg
sudo pvremove /dev/sdb
sudo pvremove /dev/sdc
```







