# IZTSDN
虚拟机操作注意事项：
1、初始化安装，需要更换源，拍初始快照

2、前期可以 su root切换到root账号
Sudo  passwd  root   可以更换新的密码

3、git的时候需要关闭全局代理
（1）取消代理
git config --global --unset http.proxy
git config --global --unset https.proxy    即可以直接拉取代码

4、Sudo 不能运行的时候，文件一般锁了，需要解锁
Sudo chmod -R 7777 文件名（最好在文件所在目录执行）

5、增加一个新用户
切换到 root
Useradd  -m 用户名
Passwd 用户名  设置新用户名的密码
删除一个用户
 Sudo userdel  -r 要删除的用户名
查看是否删除  ls -l . /home/
更改现有的用户名
登录界面直接可以点击修改
 
6、直接导出虚拟机 ovf 或者ova 都可以直接在其他虚拟机里面导入运行


进入mininet文件夹里面
 
继续进去example文件夹来启动mininet可视化界面 
 
进入界面以后可以点击图标来构建一个SDN仿真网络环境
 
从edit 选项栏中有勾选start CLI 选项来允许使用命令行
 
 
点击RUN开始运行网络环境
 
命令行开始运行，用 pingall 来测试整个网络通信状况，在以下这样的网络拓扑中，每个主机之间都是可以进行互相通信的
进/usr/local/lib/python2.7/dist-packages/mininet修改 cli.py
密钥 vyJbj2TmFLZvCBOBq07Uo1qgxMIDb4LvWyU7JhN4eJw=
 

现在需要进行初始化操作，初始化成功以后，意味着整个网络进入到初始化状态，互相之间无法通信
 


在初始化完成时，由于本项目基于零信任基础建立，所有主机之间是互相断开的状态，需要身份验证通过后方可建立连接。我们需要让他们建立连接
 
该valid命令接受三个必要参数： host1:此参数为需要建立的两台主机中的其中一台，为其名称，可通过miniedit界面查看主机名称，也可通过右键主机，选择Properties,修改Hostname修改该名称。 host2：此参数为需要建立的两台主机中的另一台，同上。 password：此参数为设置的秘钥，可通过项目目录下cli.py文件，找到SDPICSPwd参数，修改秘钥。


通过验证以后，设备之间可以进行正常的通信，通过测试发现只有验证通过的两个设备之间才能彼此通信
 

注：为确保成功运行环境，每次通信完以后需要清理流表，sudo  mn  -c 即可







以上已经完成了认证过程，接下来里需要我们通过RYU API 来实现ZTA的智能化，利用我们的已经训练好的模型来结合ZTA做一个用户行为的识别
首先来查看RYU虚拟机上面的ip
 
在mininet当中可以用命令行或者点击控制器来设置连接的ip地址，点击开始运行来实现流量的转发以及整个网络环境的正常运行
 
simple_switch_13.py模块是一个简单的交换机，是openflow1.3的交换机。后面的两个文件是为了进行restapi的调用加载的，方便直接用浏览器查看。
 
 
当我们在mininet这边网络环境进行操作的时候，流表通过RYU来控制转发，在浏览器中我们看到交换机状态信息
 
查看交换机当前的流表
 


得到端口的统计信息
 
得到端口配置信息
 



