# Raspberry Pi + Visual Studio 2019 + .NET CORE 3.1

## 本机系统环境

+ [Windows 10 (business editions), version 1909 (updated Jan 2020) (x64) - DVD (Chinese-Simplified)](ed2k://|file|cn_windows_10_business_editions_version_1909_updated_jan_2020_x64_dvd_b3e1f3a6.iso|5311711232|3527D2A9845FF4105F485CC364655B66|/ "Windows 10 (business editions), version 1909 (updated Jan 2020) (x64) - DVD (Chinese-Simplified)")
+ 激活：hwid.kms19.gen.mk4.exe（自己百度）

## 游览器

+ 使用 [Microsoft Edge 浏览器](https://www.microsoft.com/zh-cn/edge "Microsoft Edge 浏览器")
+ Microsoft Edge 浏览器,网页右键自带翻译功能，可以很好的翻译国外网站。

## 硬件

+ Raspberry Pi 4
  + [![](https://www.raspberrypi.org/homepage-9df4b/static/hero-shot-33d83b8c5fa0933373dabcc9462b32a3.png)](https://www.raspberrypi.org "Raspberry Pi 4")
  + [微雪电子](http://www.waveshare.net "微雪电子")，[BME280](http://www.waveshare.net/shop/BME280-Environmental-Sensor.htm "BME280")
  + 代码说明：[BME280](https://github.com/dotnet/iot/tree/master/src/devices/Bmxx80 "BME280")
  + 视频：[IoT 101](https://channel9.msdn.com/Series/IoT-101 "IoT 101")(视频右下角可以选择中文字幕)
  + 注意：最好使用sd卡容量大小为32G以下，支持FAT32格式，大容量存储需要强制转换。

## 系统

+ Ubuntu Server 18.04.4
  + 官方地址：[Install Ubuntu Server on a Raspberry Pi 2, 3 or 4 | Ubuntu](https://ubuntu.com/download/raspberry-pi "Install Ubuntu Server on a Raspberry Pi 2, 3 or 4 | Ubuntu")
  + 下载镜像：[Download 64-bit](https://ubuntu.com/download/raspberry-pi/thank-you?version=18.04.4&architecture=arm64+raspi3 "Download 64-bit")
  + 烧录镜像到SD卡：[balenaEtcher](https://www.balena.io/etcher "balenaEtcher")

## 配置

+ Ubuntu Server 18.04.4
  + 默认登陆账号：ubuntu
  + 默认登陆密码：ubuntu
  + 默认登陆完成需要改密码，第一次还要输入密码：ubuntu
  + 修改密码（小键盘记得开启）

+ 配置
  + 配置更新源
  + 执行命令：`sudo nano /etc/apt/sources.list`
  + 把所有网址改为[清华源](https://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports "清华源")
  + 配置wifi
  + 执行命令：`sudo nano /etc/netplan/50-cloud-init.yaml`
  + netplan说明：[netplan](https://netplan.io/examples "netplan")
  + 注意：netplan里面配置，空格需要一致，空格需要一致，空格需要一致（大坑）
  + 更新系统软件
  + 执行命令：`sudo apt-get update`
  + 执行命令：`sudo apt-get upgrade`
  + 配置时区
  + 执行命令：查看时区：`timedatectl status | grep "Time zone"`
  + 执行命令：配置时区：`sudo dpkg-reconfigure tzdata`
  + 选择：Asia/Shanghai
  + 这时可以用windows 10 系统的 CMD 命令行界面 远程登陆 Raspberry Pi

```
# 固定IP
network:
    version: 2
    renderer: networkd
    wifis:
        wlan0:
            dhcp4: no
            dhcp6: no
            addresses: [192.168.1.101/24]
            gateway4: 192.168.1.1
            nameservers:
                addresses: [114.114.114.114,8.8.8.8]
            access-points:
                "无线SID":
                  password: "无线密码"
# 自动获取IP
network:
    version: 2
    renderer: networkd
    wifis:
        wlan0:
            dhcp4: true
            access-points:
                "无线SID":
                  password: "无线密码"
```

+ windows 10 操作
  + 