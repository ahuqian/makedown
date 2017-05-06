Linux的基本命令<br>
1.ls list 显示目录下的内容<br>
2.ls 直接回车，显示目录文件<br>
3.ls -a 显示所有文件(包含隐藏文件)<br>
4.ls -hl 文件大小显示为常见单位大小<br>
5.ls -d 显示目录本身，而不是里面的子文件<br>
6.ls -l 文件名<br>
7.#超级用户 $普通用户<br>
8.cd 切换所在目录<br>
9.cd ~ 进入当前目录的家目录<br>
10.cd - 进入上一级目录<br>
11.cd .. 进入上一级目录<br>
12.cd . 进入当前目录<br>
13.pwd 显示当前所在目录<br>
14./ 根目录<br>
15./bin 命令保存目录(普通用户就可以读取的命令)<br>
16./boot 启动目录，启动相关文件<br>
17./dev 设备文件保存目录<br>
18./etc 设配文件保存目录<br>
19./home 普通用户的家目录<br>
20./mnt 系统挂载目录<br>
21./media 挂载目录<br>
22./root 超级用户的家目录<br>
23./tmp 临时目录<br>
24./sbin 命令保存目录(超级用户才能使用的目录)<br>
25./proc 直接写入内存的<br>
26./usr 系统软件资源目录<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;/usr/bin/ 系统命令(普通用户)<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;/usr/sbin/ 系统命令(超级用户)<br>
27./var 系统相关文档内容<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;/var/log/ 系统日志位置<br>
28.mkdir 目录名  创建目录<br>
29.rmdir 目录 只能删除空目录<br>
30.touch 文件名 创建空文件或修改文件时间<br>
31.rm -rf 文件名 删除<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-r 删除目录<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-f 强制删除<br>



vim 编辑器
全屏幕纯文本编辑器
vi -> vim(加强版)
三种模式：   命令模式    插入模式    末行模式
             a/i/o       ESC         :wq 保存退出 :w 保存 
                                     :q 退出  :q!不保存退出
                                     :wq! 强制保存退出（root）

光标移动  h j k l    gg 光标移动文件第一行  G 光标移动文件末行 :n 行号

设置行号:set nu   取消: set nonu  

复制 yy  nyy      

粘贴 p

删除（剪切）  x  单个字符  nx 多个字符  
     	     dd  删除行   ndd 删除多行

撤销 u    反撤销 Ctrl+r  

颜色开关（语法高亮）:syntax on    开启   :syntax off  关闭

建立配置文件 
#vim /root/.vimrc
set nu

查找  /   n 向下   N 向上

#vim index.php
替换  全文替换 :%s/echo/print/g  
      范围替换 :10,20s/print/echo/g

注释 #   //
     :5,20s/^/#/g   添加注释   :10,15s/^#//g  取消注释
     :50,70s/^/\/\//g          :60,70s/^\/\///g
 
软件包管理
软件包分类   1.源码包  .tar.gz   .tar.bz2 
             2.二进制包 .rpm

二进制包安装    rpm命令 手动管理     yum命令  自动管理
挂载光盘
#mount /dev/sr0 /mnt/cdrom
#cd /mnt/cdrom/Packages/
#ls | wc -l  统计
软件命名 ：软件名-版本号-更新次数.企业linux版本.硬件平台.rpm 
                                               i386 i686 32位 
                                               x86_64   64位
					       noarch  跨平台

1.rpm命令
1）安装 tree 目录树
#rpm -ivh  tree-tab补全
#tree     
#tree /root
#tree  /     

2）升级 -Uvh
#rpm -Uvh   软件包名称

3）卸载 -e
#rpm -e  tree   
#tree  无法执行

4）查询 -q 
#rpm  -q   tree  查询tree是否被安装
#rpm  -qa | wc -l 查询安装的二进制包数量

#rpm -qip tree-tab补全  查询未被安装的软件包的信息
#rpm -qi  tree  查询已经安装的软件包信息

#rpm -qlp tree-tab补全  查询未被安装的软件包将要安装的位置
#rpm -ql  tree   查询已经安装的软件安装的位置

#rpm -qf  /bin/ls  查询命令文件属于哪个软件包

二进制包安装 yum命令 自动化管理
#yum -y install  软件名   安装
#yum -y remove   软件名   卸载
#yum -y update   软件名   升级
#yum list  

配置yum源 
1.挂载光盘 进入yum源配置目录
#mount /dev/sr0 /mnt/cdrom/
#cd /etc/yum.repos.d/
2.修改网络yum源名称
#mv CentOS-Base.repo  CentOS-Base.repo.bak
#ls
3.配置光盘yum源
#vim CentOS-Media.repo
baseurl=file:///mnt/cdrom/
gpgcheck=0
enabled=1

测试：
#yum -y remove tree  卸载tree
#tree 确认
#yum -y install tree  安装tree
#tree 确认

安装gcc（C语言编译器）
#yum -y install gcc

xshell  远程管理工具 
xftp    远程传输工具 


源码包安装
安装httpd-2.2.29.tar.gz 
1)解压
#tar -zxvf  httpd-2.2.29.tar.gz 
#ls
2)进入解压目录
#cd httpd-2.2.29
#ls 
3)查看文件README  INSTALL
#vim README
#vim INSTALL
4)检查配置 生成文件 configure
#./configure --prefix=/usr/local/apache2/
5)编译
#make 
6)编译安装
#make install  

启动服务
关闭防火墙  #setup
关闭selinux #vim /etc/selinux/config
            SELINUX=disabled
            #reboot
#/usr/local/apache2/bin/apachectl start  启动服务

测试　浏览器　192.168.176.251   It works! 

卸载
#rm -rf /usr/local/apache2/ 

补充命令
#date  -s 20170216
#date  -s 12:08:59

#du  -sh   查看目录大小  已常见单位





















