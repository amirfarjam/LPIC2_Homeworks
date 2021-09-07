# LIPC2-05 ( Mr.Salahshoor Class Homework )

## Exercise 1
1. Download and unzip source code and then move them to /usr/local/src. 

```bash
sudo tar -xf i40e-2.16.11.tar.gz -C /usr/local/src/
sudo mv /usr/local/src/i40e-2.16.11/src /usr/src/i40e-2.16.11
```
![image1-1](assets/1-1.png)
2. make dkms.conf file
```bash
cd /usr/src/i40e-2.16.11
sudo vim dkms.conf
```
![image1-2](assets/1-2.png)
3. add dkms.conf file
```bash
sudo dkms add -m i40e -v 2.16.11
```
![image1-3](assets/1-3.png)
4. build dkms 
```bash
sudo dkms install -m i40e -v 2.16.11
```
![image1-4](assets/1-4.png)
5. get status of i40e module
```bash
dkms status |grep i40e
modeinfo i40e
```
![image1-5](assets/1-5.png)
6. remove and add i49e module 
![image1-6](assets/1-6.png)

## Exercise 2
1. copy source code from git repository 
```bash
git clone https://github.com/vicgeralds/vitetris.git
```
2. configure and make binary file for tetris game
![image2-1](assets/2-1.png)
![image2-2](assets/2-2.png)
![image2-3](assets/2-3.png)
3. run the game with ./tetris command
![image2-4](assets/2-4.png)

## Exercise 3
1. get attribute of a device with --attribute-walk option
```bash
udevadm info --attribute-walk /dev/sda
```
![image3-1](assets/3-1.png)

## Exercise 4
1. get a divice event with dmesg
```bash
sudo dmesg -T |grep usb |tail -20
```
![image4-1](assets/4-1.png)
2. get recent device events with udevadm
```bash
udevadm monitor
```
![image2-2](assets/4-2.png)


## Exercise 5
1. use lsusb to get VendorID and ProductID
```bash
lsusb
```
![image5-1](assets/5-1.png)
2. also we could use udevadm to get vendor and product IDs and serial No of a device.
```bash
udevadm info -an sde|grep inVendor
udevadm info -an sde|grep serial
```
![image5-2](assets/5-2.png)
3. create a script to write a log file when its executed.

![image5-3](assets/5-3.png)
4. create new rule in /etc/udev/rules.d folder for our usb. then we reload udev config to add our new rule.
```bash
sudo udevadm control --reload
```
![image5-4](assets/5-4.png)
5. every time we attach our usb, a new line will append to log file.

![image5-5](assets/5-5.png)
