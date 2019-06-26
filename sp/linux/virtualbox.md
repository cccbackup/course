# VirtualBox

## 在 Windows 中安裝 VirtualBox 後再安裝 Ubuntu

安裝好之後，剪貼板沒辦法用 (沒辦法剪貼進去和複製出來)

這時必須在 ubuntu 中安裝 Guest Additions，請參考下文:

Create Ubuntu server instance under VirtualBox (obviously).
Start VM, go to Devices -> Insert Guest Additions CD image to mount the ISO image.

From the terminal, run the following commands:

```
sudo -i  
apt install gcc make  
mkdir -p /media/cdrom  
mount /dev/cdrom /media/cdrom  
/media/cdrom/VBoxLinuxAdditions.run  
reboot 
```
 
After reboot:

```
sudo usermod --append --groups vboxsf USERNAME
```

Host shares should now be mounted in Ubuntu guest under /media via the installed VBoxService service, set to start on system boot-up.


* https://www.tecmint.com/install-virtualbox-guest-additions-in-ubuntu/

方法：

```
$ sudo apt update
$ sudo apt upgrade
```

然後重開機，之後下:

```
$ sudo apt install build-essential dkms linux-headers-$(uname -r)
```

接著按下 裝置 => 插入 Guest Additions 映像



1. 需要在 Ubuntu 中安裝 Guest Addition
    * sudo apt-get install virtualbox-guest-dkms
2. 需要設定《設定值/進階/共用剪貼簿》為雙向
