# iBlog2
基于 Node.js 的个人开源博客系统，采用响应式布局，支持移动设备直接访问，功能全面，美观大方。  
_不仅仅是博客，更是 Demo_，适合新人入门学习的完整项目。  

## 在线实例
个人博客 [http://www.skysun.name/](http://www.skysun.name/)

## 分支说明
当前项目分为 [master](https://github.com/eshengsky/iBlog2/tree/master) 分支和 [Jade-template](https://github.com/eshengsky/iBlog2/tree/Jade-template) 分支，唯一的区别在于 master 分支使用的是我自己写的 [Saker](https://github.com/eshengsky/saker) 模板引擎，Jade-template 分支使用的 [Jade](https://pugjs.org/) 模板引擎。

## [Wiki](https://github.com/eshengsky/iBlog2/wiki)
整理了 iBlog2 中涉及 Node.js 及部分前端技术的基本功能与知识点，适合新手学习、备查。  

## 功能模块
#### 博客
* 文章列表页  
* 文章详细页  

#### 留言
#### 关于
#### 后台管理
* 网站统计  
* 博客管理 - 新的文章  
* 博客管理 - 分类管理  
* 博客管理 - 文章管理  
* 评论管理  
* 留言管理  
* 关于管理  
* 缓存管理  
* 异常管理  
* 系统设置  

## 技术构成
* 服务端 [Node.js](https://nodejs.org/)
* web框架 [Express 4](http://expressjs.com/)
* 模板引擎 [Saker](https://github.com/eshengsky/saker) (master分支) / [Jade](https://pugjs.org/) (Jade-template分支)
* JS库 [jQuery](http://jquery.com/)
* UI库 [Bootstrap 3](http://getbootstrap.com/)
* 持久化 [MongoDB](https://www.mongodb.org/)
* 缓存（可选） [Redis](http://redis.io/)
* 日志 [winston](https://github.com/winstonjs/winston/)

## 快速开始
#### 准备条件
安装最新版[Node.js](https://nodejs.org/en/download/)、[bower](http://bower.io/)、[MongoDB](https://www.mongodb.org/downloads/)、[Redis](http://redis.io/download/)（可选）。  
（注：如果使用Windows平台，可以去[https://github.com/MSOpenTech/redis/releases](https://github.com/MSOpenTech/redis/releases)下载安装Redis）
#### 安装依赖
* 服务端依赖  
```Shell
$ npm install
```
* 客户端依赖  
```Shell
$ bower install
```

#### 参数配置
根据实际情况修改 config.json 配置文件，DbPath 是 MongoDB 路径，Redis 是缓存配置，Redis.Active 表示是否启用Redis缓存（默认不开启），Redis.Host 表示 Redis 服务器 ip 地址，Redis.Port 表示 Redis 端口号。  
```JSON
{
  "DbPath": "mongodb://localhost/iBlog2",
  "Redis": {
      "Active": false,
      "Host": "127.0.0.1",
      "Port": 6379
  }
}
```
后台管理员账号信息在 config/account.json 中配置，默认管理员账号 admin ，密码 123456 ，密码需[md5加密](http://md5jiami.51240.com/)存储。
```JSON
{
  "Id": "1",
  "UserName": "admin",
  "Password": "e10adc3949ba59abbe56e057f20f883e"
}
```
在 "后台管理-系统设置" 页面中，支持以可视化方式配置其余参数。
#### 启动站点  
*注意：对于node v4及以下版本，需要添加 --harmony-proxies 参数。*  

* 方式1：普通模式启动
```Shell
$ node ./bin/www 
```
* 方式2：快速启动
```Shell
$ npm start
```
* 方式3：守护进程启动  
_守护进程能够发挥多核CPU性能，并在出现异常退出后延迟30秒自动重启工作进程。_
```Shell
$ node daemon.js
```
打开浏览器，访问 [http://localhost:3000/](http://localhost:3000)
#### Enjoy it! :smile:

## 关于缓存
文章分类、文章列表、文章详细等都作了缓存处理，若想使修改立即可见，需要在"后台管理-缓存管理"页面手动清除缓存。

## 线上部署
推荐使用 [pm2](https://github.com/Unitech/pm2) 进行线上Node.js的进程管理和持久运行。
#### 安装
```Shell
$ npm install -g pm2
```
#### 使用
```Shell
$ pm2 start ./bin/www
```