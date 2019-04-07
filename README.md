# shadowsocks client on Ubuntu 16.04 

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
