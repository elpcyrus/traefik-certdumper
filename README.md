
### traefik

- 编辑修改 .env 文件
- 去 cloudflare 中获取域名修改权限的 token，写入到文件中：

```bash
vi cf_api_token.txt
```

负责反向代理服务器里面的应用。
自动生成和更新证书文件到 acme.json 文件中

- 更改 acme.json 权限:

```bash
chmod 600 ./data/acme.json
```

给应用服务加上安全证书

- 创建容器所需的网络：

```bash
docker network create proxy
```

- traefik-dashboard 的密钥生成：

```bash
apt install apache2-utils
echo $(htpasswd -nB admin) | sed -e s/\\$/\\$\\$/g
```

- 将 .env 中的变量替换到 data 文件夹下面的配置文件中：

```bash
export $(cat .env | xargs)  # 加载 .env 中的变量到环境
for file in ./data/*.yml; do
  envsubst < "$file" > "${file}.tmp" && mv "${file}.tmp" "$file"
done
```

### traefik certs dumper

负责监视 traefik 的证书文件 acme.json 的变更。始终将最新的证书转换成 fullchain.cer 和 private.key 文件到指定目录。

### cloudflare 的设置

获取 token
建立 A 记录
建立 CNAME 记录
关闭 cloudflare 的代理，把小云朵从橙黄色变成灰色。
