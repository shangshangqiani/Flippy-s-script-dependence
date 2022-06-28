# Flippy-s-script-dependence
本仓库主要介绍Flippy's Amlogic S9xxx 脚本依赖以及用法

openwrt源码仓库lean:https://github.com/coolsnowwolf/lede  
Amlogic S9xxx内核与脚本打包工具：https://github.com/a736399919/openwrt-s905d-n1  

## 【脚本依赖】：

```yaml
Base system--->busybox  
                      [*]Customize busybox options  
                          Linux System Utilities--->  
                          [*]fdisk  
                          [*]  Write support  
                          [*]    Support AIT disklabels  
                          [*]    Support SGI disklabels  
                          [*]    Support SUN disklabels  
                          [*]    Support BSD disklabels  
                          [*]    Support GPT disklabels  
                          [*]    Support expert mode  
                          [*]mkfs.ext2  
Utilities--->Disc--->  
                        <*>cfdisk  
                        <*>lsblk  
                  Filesystem--->  
                        <*>btrfs-progs  
                        <*>dosfstools         
                  <*>losetup  
                  <*>uuidgen  
Languages--->Perl---><*>perl  
```

## 【安装OpenWRT进emmc】：

cd /usr/sbin  
sh openwrt-install-amlogic  
Please choose:101`以Phicomm N1为例` 

## 【Emmc启动升级OpenWRT】:

将固件上传至`/mnt/mmcblk2p4`  
cd /usr/sbin  
sh openwrt-update-amlogic  
y  

## 【U盘启动升级OpenWRT】:

1.确认分区情况
<br/><br/>lsblk  
<br/><br/>看看`sda`下有没有`sda3`和`sda4`没有则执行以下命令:  
<br/><br/>cfdisk  
<br/><br/>slect--->new--->partition size:960M(primary)`创建sda3`  
<br/><br/>--->writ--->yes--->quit  
<br/><br/>slect--->new--->partition size:960M(primary)`创建sda4`  
<br/><br/>--->writ--->yes--->quit  
             
 2.确认挂载情况
<br/><br/>lsblk  
<br/><br/>如果`sda`下`sda2`挂载到`/`以及`sad4`未挂载则执行以下命令:  
<br/><br/>mkfs.ext4 /dev/sda4  
<br/><br/>mkdir /mnt/sda4  
<br/><br/>mount /dev/sda4 /mnt/sda4  
<br/><br/>如果`sda`下`sda3`挂载到`/`则执行以下命令  
<br/><br/>mount /dev/sda2 /mnt/sda3  
      
3.将固件上传至`/mnt/sda4`  
<br/><br/>cd /usr/sbin  
<br/><br/>sh openwrt-update-amlogic  
<br/><br/>y  
   
## enjoy~
 
## 鸣谢

- [OpenWrt](https://github.com/openwrt/openwrt)
- [coolsnowwolf/lede](https://github.com/coolsnowwolf/lede)
- [Lienol/openwrt](https://github.com/Lienol/openwrt)
- [unifreq/openwrt_packit](https://github.com/unifreq/openwrt_packit)
- [openwrt-s905d-n1](https://github.com/a736399919/openwrt-s905d-n1)
