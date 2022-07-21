# certbot_learn
https 证书的获取方式

## mac 系统

安装 certbot

```bash
brew install certbot
```

国内网络有点蛋疼，有科学上网方式的请打开

下载完后，就可以做泛域名手动注册

```
certbot certonly --manual -d xxxx.xxx -d "*.xxxx.xxx" --preferred-challenges dns-01 --server https://acme-v02.api.letsencrypt.org/directory
```

`-d` 后面是域名, `"*.xxxx.xxx"` 是泛域名的方式，则 test.xxxx.xxx 的都可以用这个证书

`--preferred-challenges dns-01 --server https://acme-v02.api.letsencrypt.org/directory` 这些都是固定值，大致的意思是用那个服务来注册，目前了解到的是只有 `acme-v02` 才支持泛域名

如果提示权限不够的话，自己用 `sudo` 执行

然后按照提示，输入接受通知的邮箱地址，还有同意一下他们的协议

然后需要证明你有这个域名的管理权，需要去配置一个 txt 的域名解析，大概是下面这样

```bash
Please deploy a DNS TXT record under the name:

_acme-challenge.xxxx.xxx.

with the following value:

1sAeCZFHJE6W01letAOYMLFs4331p2YG8SSdOBjr6ak
```

`txt` 的 二级域名设置为 `_acme-challenge`，`value` 值填 `1sAeCZFHJE6W01letAOYMLFs4331p2YG8SSdOBjr6ak`

设置完后等生效后按回车继续，加入校验通过的话，就可以了。

```bash
Successfully received certificate.
Certificate is saved at: /etc/letsencrypt/live/xxxx.xxx/fullchain.pem
Key is saved at:         /etc/letsencrypt/live/xxxx.xxx/privkey.pem
This certificate expires on 2022-10-19.
These files will be updated when the certificate renews.
```

有效期大概就3个月

最后可以自己通过 `cat` 命令来查看，如果没有权限一样是 `sudo` 就好了

```bash
cat /etc/letsencrypt/live/xxxx.xxx/fullchain.pem
```

