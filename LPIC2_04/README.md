# LIPC2-04 ( Mr.Salahshoor Class Homework )

## Exercise 1
1. with echo command we chenge content of initram file. 
2. as we see in pic 2-1 system could not boot 
3. we need to boot the system with live CD and fix initram file
4. then we mount some directory in filesystem and change root directory to /mnt:
```bash
sudo fdisk -l
sudo mount /dev/sdaX /mnt
sudo mount --bind /dev /mnt/dev
sudo mount --bind /proc /mnt/proc
sudo mount --bind /sys /mnt/sys
sudo chroot /mnt
```
5. now we could fix inirram file with update-initramfs command
6. finally we should update grub


![image1-1](assets/1-1.png)
![image1-2](assets/1-2.png)
![image1-3](assets/1-3.png)
![image1-4](assets/1-4.png)

## Exercise 2
1. we use "modprobe" command with "show-depends" option to list dependencies of a module
2. we could update module dependencies with "depmod" command.

![image2-1](assets/2-1.png)


## Exercise 3
1. download linux kernel version 5.14.0-rc7
2. extract tar file in /usr/src/linux folder
3. copy config file of older kernel from /boot folder to /usr/src/linux to use it as a staring point.
4. install needed program to compile kernel source code.
5.use make xconfig of make defcinfig to build config file.
6.use make command to compile kernel then copy it to /boot folder 
7.for modules I used "make modules" then "make modules-install"
8. with build initrd file with "mkinitramfs" command 
9. finally we update grub to include new kernel in boot menu.


![image3-1](assets/3-1.png)
![image3-2](assets/3-2.png)
![image3-3](assets/3-3.png)
![image3-4](assets/3-4.png)
![image3-5](assets/3-5.png)
![image3-6](assets/3-6.png)
![image3-7](assets/3-7.png)
![image3-8](assets/3-8.png)
![image3-9](assets/3-9.png)
![image3-10](assets/3-10.png)
![image3-11](assets/3-11.png)
![image3-12](assets/3-12.png)

