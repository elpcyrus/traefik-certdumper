
### traefik

负责反向代理服务器里面的应用。
自动生成和更新证书文件到 acme.json 文件中
给应用服务加上安全证书

### traefik certs dumper

负责监视 traefik 的证书文件 acme.json 的变更。始终将最新的证书转换成 fullchain.cer 和 private.key 文件到指定目录。

### cloudflare 的设置

获取 token
建立 A 记录
建立 CNAME 记录
关闭 cloudflare 的代理，把小云朵从橙黄色变成灰色。