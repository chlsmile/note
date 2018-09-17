## centos7关闭防护墙

#### centos7查看防护墙状态
```bash
firewall-cmd --state
```

#### centos7关闭防火墙
```bash
systemctl stop firewalld.service
```

#### centos7禁止防火墙开机启动
```bash
systemctl disable firewalld.service
```


#### centos7重启防火墙
```bash
systemctl restart firewalld.service
```

#### centos7启用防火墙
```bash
systemctl start firewalld.service
```
