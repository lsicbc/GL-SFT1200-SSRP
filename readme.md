# GL-iNet GL-SFT1200 路由器安装 ShadowSocksR Plus 插件

## 基于官方固件版本3.206安装SSRP插件

- 官方固件下载地址：https://dl.gl-inet.cn/?model=sft1200
- 空间不够可参考openwrt扩容overlay[将 Overlay 空间指向外置存储](https://blog.digicat-studio.com/Technology/openwrt_overlay.html)

## 安装方法
1.下载压缩包，解压密码：ssrp；

2.使用winscp工具上传插件到路由器的/tmp/tmp/目录下；

3.使用“cd /tmp/tmp/”进入插件上传目录；

4.使用“opkg update && opkg install *”命令进行安装后等待安装结束即可；

5.如果打开luci中的插件报错，再继续使用命令“opkg install luci-compat”安装luci-compat插件；

6.重新登录luci会看到“服务”菜单中有你刚刚安装的插件；

7.如果SSRP无法启动，修改/etc/init.d/shadowsocksr中的START=99。

8.如果刷淘宝反应缓慢，先查看防火墙流量分载情况，并执行以下命令关闭硬件转发加速：

    uci show firewall
    .....
    uci set firewall.@defaults[0].flow_offloading='1'
    uci set firewall.@defaults[0].flow_offloading_hw='0'
    uci commit firewall
    service firewall restart

