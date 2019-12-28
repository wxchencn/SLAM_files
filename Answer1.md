# Unit1

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

### 源代码

## 4.理解ORB-SLAM2框架
