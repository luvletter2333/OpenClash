<h1 align="center">
  <img src="https://github.com/Dreamacro/clash/raw/master/docs/logo.png" alt="Clash" width="200">
  <br>OpenClash<br>

</h1>

  <p align="center">
	<a target="_blank" href="https://github.com/Dreamacro/clash/releases/tag/v1.6.5">
    <img src="https://img.shields.io/badge/Clash-v1.6.5-blue.svg">
  </a>
  <a target="_blank" href="https://github.com/vernesong/OpenClash/tree/v0.43.01-beta">
    <img src="https://img.shields.io/badge/source code-v0.43.01--beta-green.svg">
  </a>
  <a target="_blank" href="https://github.com/vernesong/OpenClash/releases/tag/v0.43.01-beta">
    <img src="https://img.shields.io/badge/New Release-v0.43.01--beta-orange.svg">
  </a>
  </p>
  

<p align="center">
本插件是一个可运行在 OpenWrt 上的<a href="https://github.com/Dreamacro/clash" target="_blank"> Clash </a>客户端
</p>
<p align="center">
兼容 Shadowsocks、ShadowsocksR、Vmess、Trojan、Snell 等协议，根据灵活的规则配置实现策略代理
</p>
<p align="center">
- 感谢<a href="https://github.com/frainzy1477" target="_blank"> frainzy1477 </a>，本插件基于<a href="https://github.com/frainzy1477/luci-app-clash" target="_blank"> Luci For Clash </a>进行二次开发 -
</p>

# NOTICE

This is a modification of OpenClash by luvletter2333 because of my preferences and requirements.

You are welcome to use this version, but you should also know **there is no DaaS** and I have no responsibility to help you debug.

I will try my best to list all changes and its commits here.

## Change logs

- Remove Credit and Dler : 6f7e191 & b47a2de
- Enable Core IPv6 by default : 6d02e257

使用手册
---


* [Wiki](https://github.com/vernesong/OpenClash/wiki)


下载地址
---


* IPK [前往下载](https://github.com/vernesong/OpenClash/releases)


依赖
---

* luci
* luci-base
* iptables
* dnsmasq-full
* coreutils
* coreutils-nohup
* bash
* curl
* ca-certificates
* ipset
* ip-full
* iptables-mod-tproxy
* iptables-mod-extra
* libcap
* libcap-bin
* ruby
* ruby-yaml
* kmod-tun(TUN模式)
* luci-compat(Luci-19.07)
* ip6tables-mod-nat(ipv6)

```
opkg update
opkg install luci luci-base iptables coreutils coreutils-nohup bash curl ca-certificates ipset ip-full iptables-mod-tproxy iptables-mod-extra libcap libcap-bin ruby ruby-yaml 
opkg install dnsmasq-full --force-overwrite
opkg install kmod-tun luci-compat ip6tables-mod-nat 
```

编译
---


从 OpenWrt 的 [SDK](http://wiki.openwrt.org/doc/howto/obtain.firmware.sdk) 编译
```bash
# 解压下载好的 SDK
tar xjf OpenWrt-SDK-ar71xx-for-linux-x86_64-gcc-4.8-linaro_uClibc-0.9.33.2.tar.bz2
cd OpenWrt-SDK-ar71xx-*

# Clone 项目
mkdir package/luci-app-openclash
cd package/luci-app-openclash
git init
git remote add -f origin https://github.com/luvletter2333/OpenClash.git
git config core.sparsecheckout true
echo "luci-app-openclash" >> .git/info/sparse-checkout
git pull --depth 1 origin master
git branch --set-upstream-to=origin/master master

# 编译 po2lmo (如果有po2lmo可跳过)
pushd luci-app-openclash/tools/po2lmo
make && sudo make install
popd

# 开始编译

# 先回退到SDK主目录
cd ../..
make package/luci-app-openclash/luci-app-openclash/compile V=99

# IPK文件位置
./bin/ar71xx/packages/base/luci-app-openclash_0.39.7-beta_all.ipk
```

```bash
# 同步源码
cd package/luci-app-openclash/luci-app-openclash
git pull

# 您也可以直接拷贝 `luci-app-openclash` 文件夹至其他 `OpenWrt` 项目的 `Package` 目录下随固件编译

make menuconfig
# 选择要编译的包 LuCI -> Applications -> luci-app-openclash

```


许可
---


* [MIT License](https://github.com/vernesong/OpenClash/blob/master/LICENSE)
* 内核 [clash](https://github.com/Dreamacro/clash) by [Dreamacro](https://github.com/Dreamacro)
* 本项目代码基于 [Luci For Clash](https://github.com/frainzy1477/luci-app-clash) by [frainzy1477](https://github.com/frainzy1477)
* GEOIP数据库 [GeoLite2](https://dev.maxmind.com/geoip/geoip2/geolite2/) by [MaxMind](https://www.maxmind.com)
* IP检查 [MyIP](https://github.com/SukkaW/MyIP) by [SukkaW](https://github.com/SukkaW)
* 控制面板 [clash-dashboard](https://github.com/Dreamacro/clash-dashboard) by [Dreamacro](https://github.com/Dreamacro)
* 控制面板 [yacd](https://github.com/haishanh/yacd) by [haishanh](https://github.com/haishanh)
* lhie1规则 [lhie1-Rules](https://github.com/lhie1/Rules) by [lhie1](https://github.com/lhie1)
* ConnersHua规则 [ConnersHua-Rules](https://github.com/ConnersHua/Profiles/tree/master) by [ConnersHua](https://github.com/ConnersHua)
* 游戏规则 [SSTap-Rule](https://github.com/FQrabbit/SSTap-Rule) by [FQrabbit](https://github.com/FQrabbit)
* 订阅转换API [Api_Constructor](https://fndroid.github.io/api_constructor/) by [Fndroid](https://github.com/Fndroid)


