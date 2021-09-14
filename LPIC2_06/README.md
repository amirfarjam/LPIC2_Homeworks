# LIPC2-06 ( Mr.Salahshoor Class Homework )

## Exercise 1
1. make 5 disk with 2GB space in virtual box

![image1-1](assets/1-1.png)

2. with fdisk we make a partition for each disk then specify "fd" for type of partition.

```bash
fdisk /dev/sdb
```
![image1-2](assets/1-2.png)

3. make raid disk with adadm command 
```bash
mdadm --create /dev/md0 --level=6 --raid-devices=4 /dev/sdb1 /dev/sdc1 /dev/sdd1 /dev/sde1
```
![image1-3](assets/1-3.png)

4. make filesystem for raid disk them mount it
```bash
mkfs.ext4 /dev/md0

mount /dev/md0 /mnt/myraid6
```
![image1-4](assets/1-4.png)

5. add raid device to /etc/fstab

![image1-5](assets/1-5.png)

6. add mdadm.conf and update initramfs
```bash
mdadm --detail --scan --verbose > /etc/mdadm/mdadm.conf

updateinitramfs -u
```
![image1-6](assets/1-6.png)

7. add spare disk
```bash
mdadm --add /dev/md0 /dev/sdf1
```
![image1-7](assets/1-7.png)

8. update mdadm.conf to include spare disk.

![image1-8](assets/1-8.png)

## Exercise 2
1. create 4 partition

![image2-1](assets/2-1.png)

2. crate btrfs disk and mount it

```bash
mkfs.btrfs -m raid10 -d raid10 /dev/sdb1 /dev/sdb2 /dev/sdb3 /dev/sdb4
```

![image2-2](assets/2-2.png)

3. mount btrfs

```bash
mkdir /mnt/mybtrfs
mount /dev//sdb1 /mnt/mybtrfs
```
![image2-3](assets/2-3.png)

4. create subvolume

```bash
btrfs subvolume create /mnt/mybtrfs/mydocs
```
![image2-4](assets/2-4.png)

5. create snapshot

```bash
btrfs subvolume snapshot /mnt/mybtrfs/mydocs /mnt/mybtrfs/mydocs/mydocs.snap
```
![image2-5](assets/2-5.png)



## Exercise 3
1. create 3 physical volume
```bash
pvcreate /dev/sdc1 /dev/sdd1 /dev/sde1
```
![image3-1](assets/3-1.png)

2. create one volume group
```bash
vgcreate vgroup /dev/sdc1 /dev/sdd1 /dev/sde1
```
![image3-2](assets/3-2.png)

3. create 2 logical volume and filesystem
```bash
lvcreate -L 2500 -n lvol01 vgroup
lvcreate -L 1500 -n lvol02 vgroup

mkfs.ext4 -m 0 /dev/vgroup/lvol01
mkfs.ext4 -m 0 /dev/vgroup/lvol02
```
![image3-3](assets/3-3.png)

4. mount lvol01 and put some files on it then create a snapshot of it.
```bash
lvcreate --size 1G --snapshot --name mysnap /dev/vgroup/lvol01
```
![image3-4](assets/3-4.png)
5. extend lvol01, first we should unmount and inactive both lvol01 and its snapshot
```bash
lvchange -an /dev/vgroup/lvol01
lvchange -an /dev/vgroup/mysnap

lvextend -L +500 /dev/vgroup/lvol01
```
![image3-5](assets/3-5.png)

6. resize lvol01 partition
```bash
resize2fs /dev/vgroup/lvol01
```
![image3-6](assets/3-6.png)

7. restore our snapshot with lvconvert command
```bash
ulvconvert --merge /dev/vgroup/mysnap
```
![image3-7](assets/3-7.png)


