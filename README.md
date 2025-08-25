# open_chinese
宇宙免责声明：全地球人民都应注重个人隐私保护，防止黑客获取个人信息实施诈骗，欧美地区的很多人已经开始使用VPN来加密自己的网络流量。<br>
为了满足世界人民对数据安全的迫切需求，本项目收集一些自建vpn server脚本、多用户web管理面板和免费机场、节点信息。因使用本项目代码，或连接他人服务器造成的经济损失和法律风险与本项目无关。科技是一把双刃剑，技术本身无罪。

# 小白
如果你对计算机技术、网络技术、加密技术一无所知，同时又想睁眼看世界，拥抱一个更加开放、安全的网络环境，你可以先使用一些功能强大的浏览器。<br>
以下浏览器任意选择一款下载，下载完成后解压，进入解压后的文件夹，双击任意一个bat文件，按照提示操作。
|浏览器种类|适用操作系统|下载连接|
|-|-|-|
|谷歌翻墙浏览器高内核版|Windows|[点击下载](https://gitlab.com/zhifan999/fq/-/wikis/%E9%AB%98%E5%86%85%E6%A0%B8%E7%89%88)|
|火狐翻墙浏览器高内核版|Windows|[点击下载](https://gitlab.com/zhifan999/fq/-/wikis/%E7%81%AB%E7%8B%90%E9%AB%98%E5%86%85%E6%A0%B8%E7%89%88)|
|Supermium翻墙浏览器|Windows|[点击下载](https://gitlab.com/zhifan999/fq/-/wikis/Supermium%E7%BF%BB%E5%A2%99%E6%B5%8F%E8%A7%88%E5%99%A8)|
其他小白工具请访问Github公益项目 [Alvin9999/new-pac](https://github.com/Alvin9999/new-pac)

# 自建自用VPN
如果你具备一定的Linux云服务器运维能力，想要使用单台非中国大陆的公网IP云服务器，搭建VPN前后端用于个人学习和方便生活。以下内容适合你。<br>

### 传统VPN（避坑）
有些小伙伴在中国大陆搜索VPN后返回的是IPSec、OpenVPN、L2TP等传统VPN协议，这些协议是用来跨网段通信的，而不是用来做网络加密和梯子的。<br>
比如疫情期间居家办公，想要从家中访问公司内网，就可以在公司那里找一个双网段服务器，然后搭建OpenVPN。传统VPN技术与本项目无关。

### 隐匿代理协议（专为突破网络限制设计）​
如果你想要加密你的网络，流量伪装，或者突破国家对网络的封禁和限速，则需要隐匿代理协议。<br>常见的隐匿代理协议包括V2Ray (VMess/VLESS)​、ShadowSocksR、trojan、Hysteria、NaiveProxy等等。<br>
想进一步了解各种隐匿代理协议的区别，请阅读 [不同协议的区别和适用场景](https://github.com/yangjiacheng1996/open_chinese/docs/protocols.md)

### trojan后端部署
如果你使用上述的小白翻墙浏览器，高峰时期卡顿，而且如果你在公司网络中使用这种应用程序，会被监控并收到公司警告。想要加密你的电脑中所有流量，就需要操作系统级别的加密手段。使用加密客户端并配置全局代理是个不错的方法。我们先使用海外服务器部署代理协议后端服务。考虑到目前中国网警擅长捕捉SSR协议的流量，并且家用梯子一般只需要TCP加密，不需要兼容冷门协议，所以我推荐部署trojan协议！trojan协议是一个基于https的加密技术，无法被中国网警截获，非常安全！以下是部署trojan后端的方法<br>
[点击此处，查看原文链接](https://gitlab.com/zhifan999/fq/-/wikis/%E8%87%AA%E5%BB%BAtrojan%E6%9C%8D%E5%8A%A1%E5%99%A8%E6%95%99%E7%A8%8B)  <br>
我简述一下步骤
1. 材料准备：1个域名，1台海外公网ip云服务器，最好是美国云服务器。可以去闲鱼购买，很便宜。将域名通过A解析到你的服务器公网ip。
2. 登录服务器，执行以下命令：
```bash
bash -c "$(curl -fsSL https://raw.githubusercontent.com/atrandys/trojan/master/trojan_mult.sh)"
```
首次运行后，选择1，按照提示输入刚才解析的域名，但最后会报错：域名的证书不可用。再次运行上方命令，选择4修复证书。最后再次运行上方命令，选择1，输入解析的域名，设置trojan密码。

### trojan客户端
服务端部署成功后，需要在你的电脑系统中安装客户端，并配置后端服务。客户端下载地址：
1. windows系统/MacOS系统，请访问 [V2rayN 客户端官方项目地址](https://github.com/2dust/v2rayN/releases)  ，展开Assets，点击下载v2rayN-windows-64.zip 或者 v2rayN-macos-64.dmg
2. 安卓手机客户端，请访问 [V2rayNG 客户端官方项目地址](https://github.com/2dust/v2rayNG/releases) , 下载v2rayNG_1.10.19_arm64-v8a.apk
3. IOS苹果手机客户端：苹果没有开源客户端，请阅读这篇文章 [IOS小白翻墙工具](https://gitlab.com/zhifan999/fq/-/wikis/%E8%8B%B9%E6%9E%9C%E6%89%8B%E6%9C%BA%E7%BF%BB%E5%A2%99%E8%BD%AF%E4%BB%B6)

下载完成后安装，点击左上角的“配置文件”---“添加Trojan配置”，将你的后端填入并保存。启动客户端，测试连接是否成功。然后客户端底部的系统代理选择“自动配置系统代理”，路由选择“全局”或者“绕过大陆Whitelist”。<br>

### 免费后端
V2ray系列客户端可以配置多种协议的代理后端服务器，你可以配置如下免费后端，不花一分钱。
|协议|感谢老板，老板威武！|文章地址|
|-|-|-|
|v2ray|Alvin9999/new-pac|https://gitlab.com/zhifan999/fq/-/wikis/v2ray%E5%85%8D%E8%B4%B9%E8%B4%A6%E5%8F%B7|
|SSR|Alvin9999/new-pac|https://gitlab.com/zhifan999/fq/-/wikis/ss%E5%85%8D%E8%B4%B9%E8%B4%A6%E5%8F%B7|

### 免费客户端
安装就能用，速度比较慢。
|提供方|下载地址|
|-|-|
|神盾VPN|https://tpsnpv.hopto.org/tipas.apk|


### 付费后端
|厂商名称|官网地址|
|-|-|
|v2free|https://w1.v2free.cyou/|
|神盾VPN|https://cn.tipas.net 或 https://sd0501.com|


# 全屋魔法
有些极客不满足于单台电脑翻墙。想要实现全屋魔法，只要家里的任何设备接入路由器WIFI或网口就可以畅游全世界。我使用一个低功耗x86小主机安装istoreOS和Passwall插件实现这个需求，[笔记链接](https://github.com/yangjiacheng1996/open_chinese/docs/homemagic.md)

# 飞机场老板
有些人手头上有不止一台海外云服务器，想要建一个飞机场，靠翻墙赚点外快。方案在设计中。<br>
to be continued ->
