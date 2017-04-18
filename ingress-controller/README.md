如果要做高可用，可以在前面在接一层ng.
如果是现有已经有了LB的环境，只需要在LB中添加各个ingress-controller所在的IP即可

将域名解析指向vip地址即可，同时这里的域名，一定要和dashboard-ingress.yaml里面指定的host一致

nginx.conf

```xml
server {
  ...
  include /etc/nginx/conf.d/
  location /{
  proxy_pass http://exposeservices;
  }
}
```

upstream.conf

```xml
upstream exposeservices {
  server 192.168.1.1:80;
  server 192.168.1.2:80;
}
```
