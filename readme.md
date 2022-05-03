# GL-iNet GL-SFT1200 路由器安装 ShadowSocksR Plus 插件

## 基于官方固件版本3.206安装SSRP插件

## 参考并提炼以下网站信息
- 官方固件下载地址：https://dl.gl-inet.cn/?model=sft1200
- 空间不够可参考openwrt扩容overlay[将 Overlay 空间指向外置存储](https://blog.digicat-studio.com/Technology/openwrt_overlay.html)
- [GL-SFT1200官方固件一键安装魔法上网](https://www.126126.xyz/post/031/#%E5%8E%9F%E5%8E%82%E7%B3%BB%E7%BB%9F%E4%B8%80%E9%94%AE%E5%AE%89%E8%A3%85%E9%AD%94%E6%B3%95%E4%B8%8A%E7%BD%91)（实测PassWall不太好用）

## 手动安装方法
1.下载压缩包，解压密码：ssrp；

2.使用winscp工具上传插件到路由器的/tmp/tmp/目录下；

3.使用“cd /tmp/tmp/”进入插件上传目录；

4.使用“opkg update && opkg install *”命令进行安装后等待安装结束即可；

5.如果打开luci中的插件报错，再继续使用命令“opkg install luci-compat”安装luci-compat插件；

6.重新登录luci会看到“服务”菜单中有你刚刚安装的插件；

## 一键安装方法
    wget -qO- https://cdn.jsdelivr.net/gh/ericwang2006/sft1200_buddha/install.sh | sh -s ssr-plus

## 优化
1.如果SSRP无法启动，请先reboot，如还不行，尝试修改/etc/init.d/shadowsocksr中的START=99。

2.如果刷淘宝反应缓慢，先查看防火墙流量分载情况，并执行以下命令关闭硬件转发加速：

    uci show firewall
    .....
    uci set firewall.@defaults[0].flow_offloading='1'
    uci set firewall.@defaults[0].flow_offloading_hw='0'
    uci commit firewall
    service firewall restart

3.执行以下命令，关闭实时速度流量统计程序（管理网页上的关闭按钮，实际没有关闭统计程序），以改善系统负载；

    /etc/init.d/gl_tertf stop
    /etc/init.d/gl_tertf disable
    
    如需恢复，执行以下命令：
    /etc/init.d/gl_tertf enable
    /etc/init.d/gl_tertf start
