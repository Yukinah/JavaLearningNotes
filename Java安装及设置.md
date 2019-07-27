# 主页
   * [JAVA SE - 官网](https://www.oracle.com/java/technologies/java-se.html)<br>
# Raspberry Pi 与 Linux
   * Arch Linux - ARMv7
      - 参考
         + [Arch Linux - ARM](https://archlinuxarm.org/platforms/armv8/broadcom/raspberry-pi-3)<br>
# 安装
## 使用SD卡
   * [RPi Easy SD Card Setup](https://elinux.org/RPi_Easy_SD_Card_Setup)<br>
## 使用U盘
   * 参考
      + [How to boot from a USB mass storage device on a Raspberry Pi](https://www.raspberrypi.org/documentation/hardware/raspberrypi/bootmodes/msd.md)<br>
   * 其他参考（临时）
      + [抛弃SD卡，使用U盘启动树梅派3](https://www.jianshu.com/p/9fe7b427ec9a)<br>
      + [抛弃SD卡，使用U盘启动树梅派3](https://www.jianshu.com/p/9fe7b427ec9a)<br>
      + [USB启动树莓派3－Raspberry Pi](http://blog.topspeedsnail.com/archives/8814)<br>
      + [树莓派3B—完全u盘启动系统](https://www.jianshu.com/p/2ed5f1c6367b)<br>
   * 步骤
   * 问题
# 更新
  - 更新源的更换
     + 参考
        - [树莓派 Raspberry Pi 更换阿里云更新源方法](http://bbs.shumeipaiba.com/thread-5-1-1.html)<br>
     + 方法<br>
        - 步骤
           - 编辑 /etc/apt/sources.list 文件
              >1.pi@raspberrypi:\~$ sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak   #备份为 sources.list.bak
              >2.pi@raspberrypi:\~$ sudo nano /etc/apt/sources.list      #编辑sources.list  文件
           - 进入编辑界面，删除原有的内容或者用#注释掉原来的源，添加下方的源。
              >deb http://mirrors.aliyun.com/raspbian/raspbian/ wheezy main non-free contrib
              >deb-src http://mirrors.aliyun.com/raspbian/raspbian/ wheezy main non-free contrib
           - 然后使用 Ctrl+O 回车后保存文件，Ctrl+X 退出编辑器。
           - 执行  
              >pi@raspberrypi:~$ sudo apt-get update && apt-get upgrade -y       #更新系统软件 并 更新已安装的包
  - 命令
     1. #sudo apt-get update
     2. #sudo apt-get upgrade
# 卸载
  - 命令
     1. #sudo apt-get remove nginx nginx-full
     2. #sudo apt autoremove
# 管理
  - 关机<br>
     1. #sudo shutdown -h now (or sudo halt)<br>
        - 备注<br>
             + > -h means halt the system  
               > now means do it straight away. You could also add number 10 to tell it to shut down in 10 minutes. You can even give a specific time 19:45 (in 24 hour format with a : colon).
  - 重启
     1. #sudo shutdown -r now (or sudo reboot)<br>
# 设置
## 网络设置
   + 参考
      - <span id="Debian-NetworkConfiguration">[Debian-NetworkConfiguration - 开始网络相关设置之前，最好先了解这部分的内容（因目前安装的系统是Debian架构的Linux），学之前，先要总体了解网络得相关知识，比如DNS，路由等](https://wiki.debian.org/NetworkConfiguration)<br></span>
         + 其中[The resolvconf program - 是Debian的特定设置文件](https://wiki.debian.org/NetworkConfiguration#The_resolvconf_program)<br>
         + 这部分可以了解多网络的路由设置[Multiple IP addresses on one Interface](https://wiki.debian.org/NetworkConfiguration#The_resolvconf_program)<br>
      - <span id = "SettingUpaRaspberryPiAsAnAccessPointInaStandaloneNetwork">[Setting up a Raspberry Pi as an access point in a standalone network (NAT)](https://www.raspberrypi.org/documentation/configuration/wireless/access-point.md#internet-sharing)<br></span>
   + 有线网络设置
      - 参考
      - 重启网络：
         + 步骤
            - 方法1
               1. #systemctl daemon-reload<br>
               2. #sudo service networking restart
            - 方法2
               1. #/etc/init.d/networking restart - 等同 systemctl ...(服务名待查) restart
         + 查询
            - #ifconfig
   + 无线WiFi设置
      - 参考
         * [Setting WiFi up via the command line](https://www.raspberrypi.org/documentation/configuration/wireless/wireless-cli.md)<br>
         * [FreeBSD Manual Pages - wpa_supplicant.conf](https://www.freebsd.org/cgi/man.cgi?query=wpa_supplicant.conf&sektion=5&apropos=0&manpath=NetBSD+6.1.5)<br>
         * [Set up a Raspberry Pi Without an External Monitor or Keyboard](https://dev.to/wiaio/set-up-a-raspberry-pi-without-an-external-monitor-or-keyboard--c88)<br>
      - 安装时设置方法（即：Pi 尚未启动过，也无法连接）
         + Create the file in /boot. 设置方法参考：[Setting up Wifi with the Command Line](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/setting-up-wifi-with-occidentalis)  <br>
            >This approach will allow you to configure Wifi by creating and editing the file directly on the SD card in another PC. The /boot partition is FAT formatted which is readable by most PC's. So you can simply insert the SD card in a USB reader and a boot folder should show up.

            >If you create a wpa_supplicant.conf file in /boot, it will be copied to the main partition's /etc/wpa_supplicant location at boot time,replacing whatever is there. It will then be deleted from /boot, so you won't see it there if you go looking.

            >So just use whatever text editor (not word processor) you want on your PC to create the file in /boot, like this:

            >Save the file and safely remove the SD card from your PC. Put it in the Raspberry Pi and power it up. If all goes well, it should copy the file over and connect to your Wifi. <br>
      - 可以连接后的设置方法
         - 步骤   
              1. 【设置文件】所在的位置：/etc/wpa_supplicant    <br>
              2. 备份初始文件：sudo cp  wpa_supplicant.conf  wpa_supplicant.conf.org
              3. 编辑wpa_supplicant.conf文件，添加设置
                 - 方法1. sudo nano /etc/wpa_supplicant/wpa_supplicant.conf
                 - 方法2. sudo vi /etc/wpa_supplicant/wpa_supplicant.conf
              ```bash
              network={
                        ssid="testing"             # 这里 testing 是 Wifi 的名称
                        psk="testingPassword"      # 这里用明文密码，需要用 wpa_passphrase 更改为
              }
              ```
              4. 设置多个无线连接的方法：
              5. 设置密码：wpa_passphrase "testing" >> /etc/wpa_supplicant/wpa_supplicant.conf
                 - 说明：use >>  可以将修改内容写在文件末尾。
              6. 设置国家信息
                 - 说明：  
                    + >On the Raspberry Pi 3 Model B+, you will also need to set the country code, so that the 5G networking can choose the                      correct frequency bands. You can either use the raspi-config application and select the localisation option, or edit                      the  wpa_supplicant.conf file and add the following. (Note you need to replace 'GB' with the ISO code of your country. See Wikipedia for a list of country codes.)  
   country=GB  
                 - 参考：[the ISO code of your country from Wikipedia](https://en.wikipedia.org/wiki/ISO_3166-1)<br>
              5. 重置设置，（并连接指定的Wifi）：wpa_cli -i wlan0 reconfigure
              6. 查询设置好的Wifi：ifconfig wlan0
         - 重启wlan0的命令(bringing the network interface down and up again:)<br>
            + 方法1
              ```bash
                 #sudo ifconfig wlan0 down
                 #sudo ifconfig wlan0 up
              ```
            + 方法2 - 需要设置/etc/network/interface才行，否则会报错
              ```bash
                 #sudo ifdown wlan0
                 #sudo up wlan0
              ```
         - 问题
            * Wi-Fi is disabled because the country is not set.
              Use raspi-config to set the country before use.  
                 - 解决：设置国家信息：美国：country=US，中国：country=CN
      + 无线WIFI开机自动连接与静态IP地址
         - 参考
            + [how to start wireless adapter on boot](https://www.raspberrypi.org/forums/viewtopic.php?t=20290)<br>
            + [Setup Wireless LAN for Raspberry Pi](https://gist.github.com/chatchavan/3c58511e3d48f478b0c2)<br>
            + [Setting up WiFi connection - 包括静态和动态IP地址设置](https://weworkweplay.com/play/automatically-connect-a-raspberry-pi-to-a-wifi-network/)<br>
         - 设置
            + 步骤
               1. sudo nano /etc/network/interfaces
               2. add
               ```bash
                   auto wlan0
                   allow-hotplug wlan0
                   iface wlan0 inet manual
                   wpa-roam /etc/wpa_supplicant/wpa_supplicant.conf

                   iface home inet static
                   address 192.168.0.120
                   netmask 255.255.255.0
                   gateway 192.168.0.1
               ```
               3. then, in the wpa_supplicant file, added
               ```bash
                  id_str="homeOne"
               ```
   + 双网卡的路由设置
      - 参考
         + [Configuring Raspberry Pi as a Wireless-to-Wired Ethernet Island](http://www.glennklockwood.com/sysadmin-howtos/rpi-wifi-island.html)<br>
         + [WiFi to ethernet adapter for an ethernet-ready TV](https://rbnrpi.wordpress.com/project-list/wifi-to-ethernet-adapter-for-an-ethernet-ready-tv/)<br>
         + [Bridging Network Connections with Proxy ARP](https://wiki.debian.org/BridgeNetworkConnectionsProxyArp)<br>
         +[Configure Raspberry Pi for use eth0 and wlan0 at the same time](https://raspberrypi.stackexchange.com/questions/70392/configure-raspberry-pi-for-use-eth0-and-wlan0-at-the-same-time)<br>
      - 设置
         + 步骤
            - 1. 
            - 2. 
   + 热点(Hotspot)设置 - 暂未研究实现
      - 参考
         + [Raspberry Pi - Auto WiFi Hotspot Switch - Direct Connection](http://www.raspberryconnect.com/network/item/331-raspberry-pi-auto-wifi-hotspot-switch-no-internet-routing)<br>
         + [Raspberry Pi - Auto WiFi Hotspot Switch Internet](http://www.raspberryconnect.com/network/item/330-raspberry-pi-auto-wifi-hotspot-switch-internet)<br>
   + VPN 设置
      - 参考
         1. [Setup iptables for VPN and local network access only](https://www.raspberrypi.org/forums/viewtopic.php?t=43375)<br>
         2. [Pi VPN Setup for PIA with killswitch and DHCP](https://www.raspberrypi.org/forums/viewtopic.php?t=223733)<br>
   + 内网穿透
      - 参考         
         1. [How to raise NAT on the raspberry](https://www.raspberrypi.org/forums/viewtopic.php?t=199306)<br> - 权威参考见 [Setting up a Raspberry Pi as an access point in a standalone network (NAT)](#SettingUpaRaspberryPiAsAnAccessPointInaStandaloneNetwork) 的部分<br>
         2. [穿越NAT来见你-树莓派远程控制 - 仅看下即可](https://zhuanlan.zhihu.com/p/33662021)<br>
   + 问题
      - ssh连接问题  
         1. aa
            - 解决：打开: /本地用户/.ssh/ , vim known_hosts, 将与连接的IP地址 冲突的 记录 删除，然后重连。
      - DNS 问题
         1. ping: baidu.com: 域名解析暂时失败 - 参考：[temporary failure in name resolution](https://www.raspberrypi.org/forums/viewtopic.php?t=157047)<br>
            - 解决：
               + 步骤：
                  1. Open an LXTerminal window
                  2. sudo sh -c 'echo "nameserver 8.8.8.8" >> /etc/resolv.conf'
         2. 3.3 默认网关 /etc/resolv.conf 被还原清空问题
            - 解决方法1：修改 /etc/resolvconf.conf
               + 步骤：
                  1. sudo cp /etc/resolvconf.conf /etc/resolvconf.conf.org
                  2. sudo nano /etc/resolvconf.conf
                  3. 在文件最后面，添加dns服务器地址
                     - name_servers=114.114.114.114
                     - name_servers=8.8.8.8
                  4. 验证
                     - cat /etc/resolv.conf
            - 解决方法2：修改 /etc/resolvconf.conf
              + 参考：
                 - [Pi VPN Setup for PIA with killswitch and DHCP](https://www.raspberrypi.org/forums/viewtopic.php?t=223733)<br>
                 - [Raspberry Pi DNS Settings: How to Change the DNS](https://pimylifeup.com/raspberry-pi-dns-settings/)<br> - 权威参考见 [Debian-NetworkConfiguration](#Debian-NetworkConfiguration) 的部分<br>
              + 步骤：
                 1. 同上 1.
                 2. 同上 2.
                 3. 在文件最后面，添加
                    ```bash
                       name_servers=114.114.114.114
                       name_servers=8.8.8.8
                       name_servers=1.1.1.1
                       name_servers_append=1.0.0.1
                       name_server_blacklist=ROUTER-OR-LOCAL-DNS-IP-ADDRESS
                    ```
                 4. 重启：sudo reboot now
                 5. 验证：ping baidu.com
## 蓝牙设置
   + 参考：[Raspberry Pi 3 B and B+ - How to Configure Wi-Fi and Bluetooth](https://www.digikey.com/en/maker/blogs/raspberry-pi-3---how-to-connect-wi-fi-and-bluetooth)<br>
   + 蓝牙键盘
   + 蓝牙音箱
## 远程桌面设置
   * 参考
      - [VNC (Virtual Network Computing)](https://www.raspberrypi.org/documentation/remote-access/vnc/)<br>
      - [Xming X Server for Windows](https://sourceforge.net/projects/xming/)<br>
      - [Xming X Server](http://www.straightrunning.com/XmingNotes/)<br>
      - [Setup x11 forwarding on Debian](https://ssarcandy.tw/2017/03/20/Setup-x11-forwarding-on-Debian/)<br>
   * 其他参考：  
      - [3 Ways to Run a Remote Desktop on Raspberry Pi](https://eltechs.com/3-ways-to-run-a-remote-desktop-on-raspberry-pi/)<br>
   * 安装<br>
      - 1.xorg方式 - 目前使用方法<br>  
         - 步骤<br>
            a. 安装包：sudo apt-get install xorg(当前使用的方法。推荐使用) or sudo apt-get install x11-apps<br>
            b. 检查 /etc/ssh/sshd_config 中 X11Forwarding 参数，如果为 no，则更改为：yes。<br>

            ```bash
                  sudo nano /etc/ssh/sshd_config
            ```
            > Match User yourusername<br>
            > X11Forwarding yes
      - 2.xrdp方式<br>
         - 参考
            + [Raspberry Pi Remote Login with XRDP](https://www.cyberpunk.rs/raspberry-pi-remote-login-with-xrdp)<br>
         - 步骤<br>
            a. sudo apt-get install xrdp<br>
            b. sudo apt-get install  openssl-blacklist xorg-docs x11-xfs-utils guacamole<br>

               ┌───────────────────────────────────────┤ 正在设定 guacamole ├───────────────────────────────────────┐
               │                                                                                                   │
               │ The installation of Guacamole under Tomcat requires restarting the Tomcat server, as Tomcat will  │
               │ only read configuration files on startup.                                                         │
               │                                                                                                   │
               │ You can also restart Tomcat manually by running "invoke-rc.d tomcat8 restart" as root.            │
               │                                                                                                   │
               │ Restart Tomcat server?                                                                            |
            c. apache2-doc apache2-suexec-pristine | apache2-suexec-custom ghostscript-x libguac-client-telnet0  junit-doc libaopalliance-java-doc libatinject-jsr330-api-java-doc libclassworlds-java-doc libcommons-dbcp-java-doc libgeronimo-jta-1.1-spec-java libcommons-httpclient-java-doc libcommons-io-java-doc libcommons-lang-java-doc libcommons-net-java-doc libdtd-parser-java-doc ecj  libecj-java-gcj freerdp-x11 libcglib-java libjackson-json-java-doc libjaxp1.3-java-gcj libjoda-convert-java libjoda-time-java-doc libjsoup-java-doc libjsr305-java-doc groovy libgeronimo-jms-1.1-spec-java libjanino-java libjansi-java libmaven-file-management-java-doc  libmaven-shared-io-java-doc libplexus-cipher-java-doc libplexus-classworlds-java-doc libplexus-container-default-java-doc libplexus-interactivity-api-java-doc libplexus-interpolation-java-doc libplexus-sec-dispatcher-java-doc libplexus-utils-java-doc libsaxon-java-doc libstax-java-doc libwagon-java-doc libxalan2-java-doc libbsf-java libxsltc-java libequinox-osgi-java libosgi-compendium-java libosgi-core-java libqdox-java libspring-beans-java libspring-context-java libspring-core-java libspring-web-java tomcat8-admin tomcat8-docs  tomcat8-examples tomcat8-user  
            d. sudo apt-get install  vnc4server cups
  
                 建议安装：
                 colord-sensor-argyll cups-bsd foomatic-db-compressed-ppds | foomatic-db printer-driver-hpcups hplip
                 cups-pdf smbclient xpp antiword docx2txt imagemagick-doc autotrace cups-bsd | lpr | lprng enscript
                 gimp gnuplot grads graphviz hp2xx html2ps libwmf-bin mplayer povray radiance texlive-base-bin
                 transfig ufraw-batch gutenprint-locales ooo2dbk rtf2xml inkscape gutenprint-doc unpaper
               下列软件包将被【卸载】：
                 realvnc-vnc-server
         3.What is FreeNX：参考：[FreeNX](https://help.ubuntu.com/community/FreeNX)<br>

   * 连接方法
      - client端
      
      - server端
         + 步骤<br>
            1.执行下列命令
            ```bash
               export DISPLAY=192.168.0.107:0.0
               xhost + 192.168.0.107
            ```
            2.执行应用
            ```bash
               xdpyinfo |head -1
            ```
            ```bash
               xclock
            ```
            ```bash
               xeyes
            ```
   * 验证及使用
      ```bash
         sudo apt-get install iceweasel   # Iceweasel is the name given to Debian’s version of Mozilla’s Firefox browser. 
         iceweasel &
      ```   
   * 问题及解决
      - [VNC viewer failing to make connection with “channel 3: open failed: connect failed: No route to host”]()<br>
         + 解决方法<br>
         ```bash
            #grep AllowTcpForwarding /etc/ssh/sshd_config
            AllowTcpForwarding yes
         ```
      - [How can I solve “connection refused by the host computer” while trying to enter PuTTY via SSH or RealVNC?](https://www.quora.com/How-can-I-solve-connection-refused-by-the-host-computer-while-trying-to-enter-PuTTY-via-SSH-or-RealVNC)<br> 
## RaspberryPi相机设置
      - [Xclock "Warning: Missing charsets in String to FontSet conversion" in CentOS/Linux 6](http://oracleapplicationsdba4u.blogspot.com/2018/08/xclock-warning-missing-charsets-in.html)<br>
   * 参考
      - [Getting started with picamera](https://projects.raspberrypi.org/en/projects/getting-started-with-picamera)<br>
   * 其他参考
      - [Raspberry Pi 相机设置教程](https://www.rs-online.com/designspark/chi-pi-cam-setup-tutorial)<br>

## Setting up a push server - 不知是什么功能的 push server，待研究。。。
   * 参考
      - [Setting up a push server](https://www.debian.org/mirror/push_server)<br>
## 基础设置
   * 时区设置
     - 参考：
          1. [时区设置](http://blog.xuite.net/zack_pan/blog/73179035-%E5%BB%BA%E6%A7%8BRaspberry+Pi+with+Arch+Linux+ARM)<br>
          2. [Raspberry Pi開發環境安裝](http://webb0219.pixnet.net/blog/post/88134014-%5Braspberry-pi%5D-%E9%96%8B%E7%99%BC%E7%92%B0%E5%A2%83%E5%AE%89%E8%A3%9D)<br>
     
     - 步骤：
        1. mv /etc/localtime /etc/localtime.old
        2. ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
  *  設定時間同步
     - 参考
     - 步骤
        1. sudo nano /etc/ntp.conf
