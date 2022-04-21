# GL-iNet GL-SFT1200 路由器安装 ShadowSocksR Plus 插件

## 基于官方固件版本3.206安装SSRP插件

- 官方固件下载地址：https://dl.gl-inet.cn/?model=sft1200
- 空间不够可参考openwrt扩容overlay[将 Overlay 空间指向外置存储](https://blog.digicat-studio.com/Technology/openwrt_overlay.html)

## 安装方法
    1.使用winscp工具上传插件到路由器的/tmp/tmp/目录下；

    2.使用“cd /tmp/tmp/”进入插件上传目录；

    3.使用“opkg update && opkg install *”命令进行安装后等待安装结束即可；

    4.遇到报错：openssl20150806已经安装，按照第5步卸载openssl20150806；

    5.在luci管理界面——软件包——过滤器——输入“libustream”——installed——删除“libustream-openssl20150806”；

    6.如果打开luci中的插件报错，再继续使用命令“opkg install luci-compat”安装luci-compat插件；

    7.重新登录luci会看到“服务”菜单中有你刚刚安装的插件。

    8.如果SSRP无法启动，修改/etc/init.d/shadowsocksr中的START=99
