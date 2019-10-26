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
 "server":"{your_server}",
 "server_port":{your_server_port},
 "local_address":"{your-server}",
 "local_port":10800,
 "password":"{your_password}",
 "timeout":600,
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

add `nohup ss-local >/dev/null 2>&1 &` before `exit 0`



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
sudo /etc/init.d/polipo restart
```

- ENV（Add to ~/.bashrc）
```json
export HTTP_PROXY=http://127.0.0.1:8123
export HTTPS_PROXY=https://127.0.0.1:8123
```
```json
git config --global http.proxy socks5://localhost:10800
git config --global https.proxy socks5://localhost:10800
```
```json
git config --global --unset http.proxy
git config --global --unset https.proxy
```

- Test if socks5 can connect google

```json
curl www.google.com
```
