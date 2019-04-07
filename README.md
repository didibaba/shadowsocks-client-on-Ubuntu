# Ubuntu 16.04配置shadowsocks client

## Install from PPA

```bash
sudo apt-get install software-properties-common -y
sudo add-apt-repository ppa:max-c-lv/shadowsocks-libev -y
sudo apt-get update
sudo apt install shadowsocks-libev
```

## Config

```bash
sudo vim /etc/shadowsocks-libev/config.json
```

```json
{
 "server":"ukss.southeastasia.cloudapp.azure.com",
 "server_port":22557,
 "local_address":"127.0.0.1",
 "local_port":10800,
 "password":"(2WHPaS$w0rd)",
 "timeout":60,
 "method":"aes-256-cfb"
}
```

```bash
sudo ss-local -c /etc/shadowsocks-libev/config.json
```
or for default `sudo vim /etc/default/shadowsocks-libev`
```bash
sudo ss-local
```

## start-up

```bash
sudo vim /etc/rc.local
```

add `sudo ss-local` before `exit 0`



## Config google chrome

## Global proxy

- 安装polipo
```bash
sudo apt-get install polipo
```

- 增加配置文件
```bash
sudo vim /etc/polipo/config
```

- add
```json
logSyslog = true
logFile = /var/log/polipo/polipo.log
proxyAddress = "0.0.0.0"
socksParentProxy = "127.0.0.1:10800"
socksProxyType = socks5
chunkHighMark = 50331648
objectHighMark = 16384
serverMaxSlots = 64
serverSlots = 16
serverSlots1 = 32
```

- 重启polipo服务
```json
sudo service polipo restart
```

- 设置环境变量（可添加至~/.bashrc文件中使所有shell均可实现全局SOCKS5访问）

```json
export HTTP_PROXY="http://127.0.0.1:8123"
export HTTPS_PROXY="https://127.0.0.1:8123"
```
但是这样git clone 就用不了了，必须

```bash
unset HTTP_PROXY
unset HTTPS_PROXY
```

- 检测一下是否可以通过socks5协议获取google主页面

```json
curl www.google.com
```
