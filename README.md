# Ubuntu shadowsocks client

## Install from PPA

Shadowsocks-libev is included in Ubuntu repository since 17.04.

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
    "server":["$your_server", "127.0.0.1"],
    "mode":"tcp_and_udp",
    "server_port":$your_server_port,
    "local_port":10800,
    "password":"$your_password",
    "timeout":600,
    "method":"aes-256-gcm"
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

## Using proxy in terminal

- Install proxychains
```bash
sudo apt install proxychains
```
- Config proxychains
```bash
sudo vim /etc/proxychains.conf
```
Remove default ProxyList content
Add "socks5 127.0.0.1 10800" to ProxyList

- Use proxychains
```bash
proxychains git clone xxxxxxxxx
```
## Using proxy in WSL 2

- Add following commands to ~/.bashrc
```bash
host_ip=$(cat /etc/resolv.conf |grep "nameserver" |cut -f 2 -d " ")
export ALL_PROXY="http://$host_ip:10800"
```
```bash
source ~/.bashrc
```

## Test if socks5 can connect google

```bash
curl www.google.com
```
