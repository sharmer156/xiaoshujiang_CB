---
title: 2024-9-17npm install设置代理服务器 镜像源
tags: 
grammar_cjkRuby: true
---


npm install 时由于会默认访问外网，所以网速很慢，可以通过配置代理或镜像源的方式间接实现install。

> 代理：是设置代理服务器，代理服务器帮你转发下载请求；
> 镜像源：是镜像站点已经提前镜像(下载)了所有的npm包，你是直接从它的服务器上获取到的包。

## 设置代理

```
npm config set proxy=http://127.0.0.1:8087

```

## 设置镜像源

```
npm config set registry=http://registry.npmjs.org

```

## 关于http

经过上面设置使用了http开头的源，因此不需要设http_proxy了，否则还要加一句

```
npm config set https-proxy http://server:port

```

## 代理用户名和密码

```
npm config set proxy http://username:password@server:port
npm config set https-proxy http://username:passwprd@server:port

```

## 查看npm config

```
npm config get

```

## 取消代理或源

```
npm config delete proxy
npm config delete https-proxy
npm config delete registry
```

作者：jiaming_
链接：https://www.jianshu.com/p/9568a519476c
来源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。