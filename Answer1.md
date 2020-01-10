# Unit1
- [Unit1](#unit1)
  - [<ul>
<li>4.理解ORB-SLAM2框架</li>
</ul>](#ul-li4%e7%90%86%e8%a7%a3orb-slam2%e6%a1%86%e6%9e%b6li-ul)
  - [1.熟悉Linux](#1%e7%86%9f%e6%82%89linux)
    - [1.1 如何在Ubuntu 中安装软件（命令⾏界⾯）？它们通常被安装在什么地⽅？](#11-%e5%a6%82%e4%bd%95%e5%9c%a8ubuntu-%e4%b8%ad%e5%ae%89%e8%a3%85%e8%bd%af%e4%bb%b6%e5%91%bd%e4%bb%a4%e2%be%8f%e7%95%8c%e2%be%af%e5%ae%83%e4%bb%ac%e9%80%9a%e5%b8%b8%e8%a2%ab%e5%ae%89%e8%a3%85%e5%9c%a8%e4%bb%80%e4%b9%88%e5%9c%b0%e2%bd%85)
    - [1.2 linux 的环境变量是什么？我如何定义新的环境变量？](#12-linux-%e7%9a%84%e7%8e%af%e5%a2%83%e5%8f%98%e9%87%8f%e6%98%af%e4%bb%80%e4%b9%88%e6%88%91%e5%a6%82%e4%bd%95%e5%ae%9a%e4%b9%89%e6%96%b0%e7%9a%84%e7%8e%af%e5%a2%83%e5%8f%98%e9%87%8f)
    - [1.3 linux 根⽬录下⾯的⽬录结构是什么样的？⾄少说出3个⽬录的⽤途。](#13-linux-%e6%a0%b9%e2%bd%ac%e5%bd%95%e4%b8%8b%e2%be%af%e7%9a%84%e2%bd%ac%e5%bd%95%e7%bb%93%e6%9e%84%e6%98%af%e4%bb%80%e4%b9%88%e6%a0%b7%e7%9a%84%e2%be%84%e5%b0%91%e8%af%b4%e5%87%ba3%e4%b8%aa%e2%bd%ac%e5%bd%95%e7%9a%84%e2%bd%a4%e9%80%94)
    - [1.4 给a.sh加上可执行权限，该输入什么命令？](#14-%e7%bb%99ash%e5%8a%a0%e4%b8%8a%e5%8f%af%e6%89%a7%e8%a1%8c%e6%9d%83%e9%99%90%e8%af%a5%e8%be%93%e5%85%a5%e4%bb%80%e4%b9%88%e5%91%bd%e4%bb%a4)
    - [1.5 将a.sh文件的所有者改成xiang:xiang，该输入什么命令？](#15-%e5%b0%86ash%e6%96%87%e4%bb%b6%e7%9a%84%e6%89%80%e6%9c%89%e8%80%85%e6%94%b9%e6%88%90xiangxiang%e8%af%a5%e8%be%93%e5%85%a5%e4%bb%80%e4%b9%88%e5%91%bd%e4%bb%a4)
  - [2.SLAM综述文献阅读](#2slam%e7%bb%bc%e8%bf%b0%e6%96%87%e7%8c%ae%e9%98%85%e8%af%bb)
    - [2.1 SLAM会在哪些应用场合中用到？](#21-slam%e4%bc%9a%e5%9c%a8%e5%93%aa%e4%ba%9b%e5%ba%94%e7%94%a8%e5%9c%ba%e5%90%88%e4%b8%ad%e7%94%a8%e5%88%b0)
    - [2.2 SLAM中定位和建图的关系？](#22-slam%e4%b8%ad%e5%ae%9a%e4%bd%8d%e5%92%8c%e5%bb%ba%e5%9b%be%e7%9a%84%e5%85%b3%e7%b3%bb)
    - [2.3 SLAM发展历史分为几个阶段？](#23-slam%e5%8f%91%e5%b1%95%e5%8e%86%e5%8f%b2%e5%88%86%e4%b8%ba%e5%87%a0%e4%b8%aa%e9%98%b6%e6%ae%b5)
    - [2.4 SLAM领域的经典文章](#24-slam%e9%a2%86%e5%9f%9f%e7%9a%84%e7%bb%8f%e5%85%b8%e6%96%87%e7%ab%a0)
  - [3.CMake 练习](#3cmake-%e7%bb%83%e4%b9%a0)
  - [4.理解ORB-SLAM2框架](#4%e7%90%86%e8%a7%a3orb-slam2%e6%a1%86%e6%9e%b6)
---
## 1.熟悉Linux

### 1.1 如何在Ubuntu 中安装软件（命令⾏界⾯）？它们通常被安装在什么地⽅？
- sudo apt install xxx
- /usr/share and /usr/local

### 1.2 linux 的环境变量是什么？我如何定义新的环境变量？
- /etc/profile //对所有用户生效 (永久)
- ~/.bashrc //对当前用户生效
- export 变量名=变量值 //对当前shell生效 (临时)

### 1.3 linux 根⽬录下⾯的⽬录结构是什么样的？⾄少说出3个⽬录的⽤途。

**/ 根目录**

| 目录              | 功能                               |
| ----------------- | ---------------------------------- |
| /bin              | 存放系统命令                       |
| /boot             | 系统启动目录                       |
| /dev              | 设备文件保存位置                   |
| /etc              | 配置文件保存位置                   |
| /home             | home目录                           |
| /lib              | 系统调用函数库                     |
| /media /mnt /misc | 挂载目录                           |
| /opt              | 第三方软件保存位置                 |
| /root             | root目录                           |
| /sbin             | 与系统环境设置相关命令；仅root使用 |
| /srv              | 服务数据目录                       |
| /tmp              | 临时目录                           |

**/usr 的子目录**
<table>
   <tr>
      <td>/usr子目录</td>
      <td>功能（作用）</td>
   </tr>
   <tr>
      <td>/usr/bin/</td>
      <td>存放系统命令，普通用户和超级用户都可以执行。这些命令和系统启动无关，在单用户模式下不能执行</td>
   </tr>
   <tr>
      <td>/usr/sbin/ </td>
      <td>存放根文件系统不必要的系统管理命令，如多数服务程序，只有 root 可以使用。</td>
   </tr>
   <tr>
      <td>/usr/lib/</td>
      <td>应用程序调用的函数库保存位置</td>
   </tr>
   <tr>
      <td>/usr/XllR6/</td>
      <td>图形界面系统保存位置</td>
   </tr>
   <tr>
      <td>/usr/local/</td>
      <td>手工安装的软件保存位置。我们一般建议源码包软件安装在这个位置</td>
   </tr>
   <tr>
      <td>/usr/share/</td>
      <td>应用程序的资源文件保存位置，如帮助文档、说明文档和字体目录</td>
   </tr>
   <tr>
      <td>/usr/src/</td>
      <td>源码包保存位置。我们手工下载的源码包和内核源码包都可以保存到这里。不过笔者更习惯把手工下载的源码包保存到 /usr/local/src/ 目录中，把内核源码保存到 /usr/src/linux/ 目录中</td>
   </tr>
   <tr>
      <td>/usr/include</td>
      <td>C/C++ 等编程语言头文件的放置目录</td>
   </tr>
</table>

**/var 的子目录**

<table>
   <tr>
      <td>/var子目录</td>
      <td>功能（作用）</td>
   </tr>
   <tr>
      <td>/var/lib/</td>
      <td>程序运行中需要调用或改变的数据保存位置。如 MySQL 的数据库保存在 /var/lib/mysql/ 目录中</td>
   </tr>
   <tr>
      <td>/var/log/</td>
      <td>登陆文件放置的目录，其中所包含比较重要的文件如 /var/log/messages, /var/log/wtmp 等。</td>
   </tr>
   <tr>
      <td>/var/run/</td>
      <td>一些服务和程序运行后，它们的 PID（进程 ID）保存位置</td>
   </tr>
   <tr>
      <td>/var/spool/</td>
      <td>里面主要都是一些临时存放，随时会被用户所调用的数据，例如 /var/spool/mail/ 存放新收到的邮件，/var/spool/cron/ 存放系统定时任务。</td>
   </tr>
   <tr>
      <td>/var/www/</td>
      <td>RPM 包安装的 Apache 的网页主目录</td>
   </tr>
   <tr>
      <td>/var/nis和/var/yp</td>
      <td>NIS 服务机制所使用的目录，nis 主要记录所有网络中每一个 client 的连接信息；yp 是 linux 的 nis 服务的日志文件存放的目录</td>
   </tr>
   <tr>
      <td>/var/tmp</td>
      <td>一些应用程序在安装或执行时，需要在重启后使用的某些文件，此目录能将该类文件暂时存放起来，完成后再行删除</td>
   </tr>
</table>

### 1.4 给a.sh加上可执行权限，该输入什么命令？
- 三种权限 <b>R</b>ead <b>W</b>rite e<b>X</b>ecute
- **chmod mode file;** example: chmod a+x a.sh
  - u表示拥有者，g表示拥有者group全体，o表示others，a表示all
  - \+ 表示增加权限、- 表示取消权限、= 表示唯一设定权限
  - r 表示可读取，w 表示可写入，x 表示可执行
- **chmod abc file;** example: chmod 777 a.sh
  - a,b,c各位一个数字，分别表示User、Group、Other的权限
  - r = 4, w = 2, x = 1

### 1.5 将a.sh文件的所有者改成xiang:xiang，该输入什么命令？
- chown [-R] name file

## 2.SLAM综述文献阅读

### 2.1 SLAM会在哪些应用场合中用到？
- 增强现实
- 机器人导航
- 自动驾驶

### 2.2 SLAM中定位和建图的关系？
定位和建图可以看成感知的内外两部分，定位是明白自身的状态，建图是了解外在的环境。

### 2.3 SLAM发展历史分为几个阶段？
- Classical age [1986-2004]
  - 基于EKF、RB粒子滤波、最大似然估计的方法
- Algorithmic-analysis age [2004-2015]
- Current state

### 2.4 SLAM领域的经典文章
- [1] H. Liu, G. Zhang, and H. Bao, “A survey of monocular simultaneous localization and mapping,” Jisuanji Fuzhu Sheji Yu Tuxingxue Xuebao/Journal Comput. Des. Comput. Graph., vol. 28, no. 6, pp. 855–868, 2016.
- [2] C. Cadena et al., “Past, present, and future of simultaneous localization and mapping: Toward the robust-perception age,” IEEE Trans. Robot., vol. 32, no. 6, pp. 1309–1332, 2016.
- [3] J. Fuentes-Pacheco, J. Ruiz-Ascencio, and J. M. Rendón-Mancha, “Visual simultaneous localization and mapping: a survey,” Artif. Intell. Rev., vol. 43, no. 1, pp. 55–81, 2012.

## 3.CMake 练习

参考SLAM十四讲(第二版)内容 [Page 30]

## 4.理解ORB-SLAM2框架

