# Ubuntu shadowsocks client

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
 "server":"$your_server",
 "server_port":$your_server_port,
 "local_address":"$your-server",
 "local_port":10800,
 "password":"$your_password",
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

## Using proxy in terminal

- Install proxychains
```bash
sudo apt install proxychains
```
- Config proxychains
```bash
sudo vim /etc/proxychains.conf
```
Add "socks5 127.0.0.1 10800" to ProxyList

- Use proxychains
```bash
proxychains git clone xxxxxxxxx
```

## Global proxy

- Install privoxy
```bash
sudo apt-get install proxychains
```

- Edit config file
```bash
sudo vim /etc/privoxy/config
```
Find the section 5.2. forward-socks4, forward-socks4a, forward-socks5 and forward-socks5t, plus the following configuration:
```bash
forward-socks5 / 127.0.0.1:10800 .
```

- Restart privoxy service
```json
sudo /etc/init.d/privoxy restart
```

- ENV（Add to ~/.bashrc）
```json
export http_proxy=http://127.0.0.1:8118
export https_proxy=https://127.0.0.1:8118
```
```json
git config --global http.proxy socks5://localhost:8118
git config --global https.proxy socks5://localhost:8118

git config --global http.https://github.com.proxy socks5://127.0.0.1:8118
git config --global https.https://github.com.proxy socks5://127.0.0.1:8118
```
```json
git config --global --unset http.proxy
git config --global --unset https.proxy
```

- Test if socks5 can connect google

```json
curl www.google.com
```
