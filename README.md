# Ubuntu 16.04 shadowsocks client

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
 "server":"***",
 "server_port":***,
 "local_address":"***",
 "local_port":10800,
 "password":"***",
 "timeout":60,
 "method":"***"
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

![chrome_img](https://github.com/didibaba/shadowsocks-client-on-Ubuntu-16.04/blob/master/web/chrome.png)

## Global proxy

- Install polipo
```bash
sudo apt-get install polipo
```

- Edit config file
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

- Restart polipo service
```json
sudo service polipo restart
```

- ENV（Add to ~/.bashrc）
```json
export HTTP_PROXY="socks5://127.0.0.1:10800"
export HTTPS_PROXY="socks5://127.0.0.1:10800"
```

- Test if socks5 can connect google

```json
curl www.google.com
```
