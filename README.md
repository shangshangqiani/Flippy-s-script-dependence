# Flippy-s-script-dependence
本仓库主要介绍Flippy's Amlogic S9xxx 脚本依赖以及用法

openwrt源码仓库lean:https://github.com/coolsnowwolf/lede
Amlogic S9xxx内核与脚本打包工具：https://github.com/a736399919/openwrt-s905d-n1

## 【脚本依赖】：

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

## 【安装OpenWRT进emmc】：

cd /usr/sbin
sh openwrt-install-amlogic
Please choose:101（Phicomm N1为例）

## 【Emmc启动升级OpenWRT】:

将固件上传至 /mnt/mmcblk2p4
cd /usr/sbin
sh openwrt-update-amlogic
y

## 【U盘启动升级OpenWRT】:

1、lsblk
   看看sda下有没有sda3和sda4没有则执行以下命令:
   cfdisk
      slect--->new--->partition size:960M(primary)【创建sda3】
             --->writ--->yes
      slect--->new--->partition size:960M(primary)【创建sda4】
             --->writ--->yes
             
 2、lsblk
   如果sda下"sda2"挂载到"/ "以及"sad4"未挂载则执行以下命令:
      mkfs.ext4 /dev/sda4
      mkdir /mnt/sda4
      mount /dev/sda4 /mnt/sda4
   如果sda下"sda3"挂载到"/"则执行以下命令
      mount /dev/sda2 /mnt/sda3
      
3、将固件上传至 /mnt/sda4
   cd /usr/sbin
   sh openwrt-update-amlogic
   y
   
## enjoy~
 
## 鸣谢

- [OpenWrt](https://github.com/openwrt/openwrt)
- [coolsnowwolf/lede](https://github.com/coolsnowwolf/lede)
- [Lienol/openwrt](https://github.com/Lienol/openwrt)
- [unifreq/openwrt_packit](https://github.com/unifreq/openwrt_packit)
- [openwrt-s905d-n1](https://github.com/a736399919/openwrt-s905d-n1)
