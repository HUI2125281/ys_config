# 感谢大白，我们好好学习一下

现状：有一个Japan的vps，装了v2ray+nginx ,可以用客户端科学上网，为了方便分流以及，准备采用1.v2ray server <-> 2.byst server <-> 3.byst client <-> 4.v2ray client的方式
其中1，2安装在vps上，3，4，安装在本地。

服务器ip假如是1.2.3.4，域名是xxx.abc.com

## 服务器端
* 服务器端程序上传后配置权限
* 修改conf.ini，主要关注一下几条
```sh
...
# Change Mode to Server on BYST Server deployment
Mode:STRING=Server
...
[Tunnels\HTTP]
Listen Addr:STRING=127.0.0.1:8080 #服务器提供服务的端口
#Connect To:STRING=107.148.250.167:443 / 149.129.108.251:995
Connect To:STRING=xxx.abc.com:443  #原来提供v2ray服务的端口
```
* 在程序目录运行
```sh
./debug
```
将生成的byst.req，发给大白，得到许可放在conf.ini的第一行

## 客户端

支持多种客户端，Windows、Linux、openwrt、MacOS、Android ，多看手册第三章
同样需要修改conf.ini，关注如下几行。
```sh
...
# Change Mode to Server on BYST Server deployment
Mode:STRING=Client
...
[Tunnels\HTTP]
Listen Addr:STRING=127.0.0.1:1088 #本地提供服务的端口
#Connect To:STRING=107.148.250.167:443 / 149.129.108.251:995
Connect To:STRING=xxx.abc.com:8080  #服务器端BYST 提供服务的端口
```
