# 部署trojan后端程序
1.需要一台香港或海外的VPS服务器或ECS云服务器，中国大陆的服务器无效。您可以点击右侧链接购买永久香港vps，一次付费，终身使用：[天霆网络VPS](https://www.idc35.com/cloud/hktehui) 。买到VPS后，系统选择Linux，尝试用ssh工具登录VPS。
2.购买一个域名。有很多购买域名的渠道，比如阿里云、gname等等。将vps的公网ip解析到域名中，记住刚解析的这个域名，比如我的是trojan.lolicloud.com 。
3.执行以下bash命令，部署trojan，会占用80和443端口。[翻墙原项目地址](https://github.com/Alvin9999/new-pac/)

```
bash -c "$(curl -fsSL https://raw.githubusercontent.com/atrandys/trojan/master/trojan_mult.sh)"

=======================================
介绍: 一键安装trojan
系统: centos7+/debian9+/ubuntu16.04+
作者: A
注意:
*1. 不要在任何生产环境使用此脚本
*2. 不要占用80和443端口
*3. 若第二次使用脚本，请先执行卸载trojan
=======================================
1. 安装trojan
2. 卸载trojan
3. 升级trojan
4. 修复证书
0. 退出脚本
请输入数字 :  


```
先选择1，输入刚解析的域名，第一次安装会失败。
重新执行命令，回到输入数字界面，选择4修复证书，输入刚解析的域名。
最后再回到输入数字界面，选择1，输入刚解析的域名，并设置一个密码。等待创建成功。

# 软路由连接trojan
1. 去淘宝上购买倍控N100软路由，cpu是x86架构，插入4800MHz内存和M.2固态硬盘。
2. 用rufus软件将istoreOS的系统镜像iso文件烧录到U盘中。[点击链接下载iso文件](https://fw.koolcenter.com/iStoreOS/x86_64_efi/) 。你也可以用ventory制作U盘启动盘，然后直接将iso文件复制到U盘根目录中即可。[点击链接下载ventory工具](https://www.ventoy.net/cn/download.html)
3. U盘插入软路由，bios中设置优先启动U盘，开机，根据提示安装istoreOS。[istoreOS安装教学视频](https://www.bilibili.com/video/BV1qz4y1n7pu/?share_source=copy_web&vd_source=4cee0005e63af504f1a4e5f79e975468)
4. 确保家里的光猫是dhcp模式，而不是桥接模式。dhcp模式下，手机连接光猫的WiFi可以直接上网，设备用网线连接光猫也可以直接上网。桥接模式下，需要接入一个路由器并输入宽带账号进行PPPOE拨号。
5. 用网线将软路由接入光猫，登录istoreOS网页，默认ip是192.168.100.1，用户名密码是root和password。在网页中，你可以设置你的路由器
6. 安装passwall插件用于翻墙。使用ssh工具登录istoreOS命令行，执行下方命令下载安装passwall插件。
```
# 下载
wget https://github.com/AUK9527/Are-u-ok/raw/main/x86/all/PassWall_4.78-1_x86_64_all_sdk_22.03.7.run
# 安装
bash PassWall_4.78-1_x86_64_all_sdk_22.03.7.run
```
7. 回到istoreOS网页，在左侧栏点击服务，可以看到第一个就是Passwall，安装成功。
8. 在Passwall中添加你的trojan后端。在istoreOS网页中点击服务->Passwall->节点列表->添加。完成表格中的配置项：

|配置项|解释|举例|
|-|-|-|
|节点备注|给你即将添加的这个trojan后端节点起一个名字|my-trojan|
|类型|选择你后端的网络协议，我们部署的是trojan，那就在下拉框中选择Trojan|Trojan-Plus|
|地址（支持域名）|就是你部署trojan时设置的域名|trojan.lolicloud.cn|
|端口|trojan后端的网络端口，我们用了一键部署脚本，默认配置就是443|443|
|密码|部署trojan后端时你设置的连接密码|asdfghjkl|
|TCP 快速打开|不用管它|false|
|TLS|是否使用https，我们部署trojan的时候是有证书的，而且trojan的原理就是使用https进行翻墙和加密，避开中国警方的监听和拦截|勾选|
|其他选项|不用管它|不用管它|

点击保存并应用。回到Passwall->基本设置，勾选“主开关”，然后tcp和udp都选择刚才添加的节点，点击保存并应用。
9. 测试是否翻墙成功。回到Passwall->基本设置，点击上方的谷歌连接、Github连接、instagram连接。这三项都变成绿色表示翻墙成功。现在你的全家人只要连接这个路由器都能访问全世界的网络，不再被屏蔽。


# 后期升级
1. 软路由没有wifi怎么办？可以去淘宝上买一个“无线AP”，用网线连接到软路由就有wifi了，而且wifi的速度取决于你的无线AP有多快。考虑到N100软路由的网口是2.5Gb的带宽，那么可以选择3000Mb的无线AP。
2. 软路由性能不足怎么办？N100软路由cpu够强了，属于酷睿i3的12代cpu，理论上支持500个设备同时在线。如果性能不足，就换更大的x86电脑，istoreOS中将子网掩码改小一点，比如20。特殊情况甚至可以用服务器。
3. 网口不足怎么办？倍控N100软路由有4网口和6网口版本，如果家里设备多，网口不够用，可以购买非管理型交换机，又叫“傻瓜式交换机”，这个很便宜的。
