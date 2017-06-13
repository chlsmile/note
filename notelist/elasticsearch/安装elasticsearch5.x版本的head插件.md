## 安装5.x版本elasticsearch的head插件
### 简介
> elasticsearch5.X版本不再支持直接集成第三方插件，如果想继续使用第三方插件可以查询一下第三方插件是否能够直接独立部署，这里选择的head插件支持直接部署(依赖node服务)，在head的github上有介绍说明


#### 安装node
```
cd /usr/local/

wget https://nodejs.org/dist/v6.11.0/node-v6.11.0.tar.gz

cd node-v6.11.0/

./configure

make

make install
```

#### 安装cnpm
在国内使用npm安装elasticsearch-head插件时由于网络被墙问题可能会导致失败，因此可以使用淘宝的npm镜像cnpm，然后可以像使用npm一样使用cnpm

```
npm install cnpm -g --registry=https://registry.npm.taobao.org
```

#### 安装elasticsearch-head
```
git clone git://github.com/mobz/elasticsearch-head.git

cd elasticsearch-head

cnpm install

cnpm run start
```



#### 参考相关文档链接
- [elasticsearch-head](<https://github.com/mobz/elasticsearch-head>)
- [淘宝npm镜像](<https://npm.taobao.org/>)
- [cnpm](<https://github.com/cnpm/cnpm>)
- [node](<https://nodejs.org/en/>)

