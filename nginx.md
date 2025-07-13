# Nginx

## Web 服务器基本概念

Web服务器指的是（world wide web）服务器，也是 HTTP 服务器，主要用于提供网上信息浏览；

Web服务器是一种被动访问的应用程序，即只有接收到互联网中其他主机发出的请求后才会响应，
最终用于提供服务程序的Web服务器会通过 HTTP/HTTPS 把请求的内容传送给用户

常见的Web服务器有： `Nginx` `Apache` `Tomcat` `Lighttpd`

## Nginx 基本概念

高性能的 HTTP 服务器、反向代理服务器

Nginx以高效的epoll、kqueue、eventport作为网络IO模型，在高并发的场景下，Nginx能够轻松支持5w并发连接数的响应
并且消耗的服务器内存、CPU等系统资源消耗很低

想让Nginx支持高并发需要做很多优化：
**优化思路**
1. 优化硬件 （服务器内存、CPU、硬盘使用SSD、使用SAS企业级硬盘、安装光纤网口）
2. 优化linux内核 （优化linux内核参数， 对TCP连接的设置、设置 `nginx.conf` 中并发的相关参数，
    如 `worked_processes 16` `worker_connections 50000`）
3. 优化nginx配置文件参数


## 生成Nginx配置文件网站

可根据你的需求生成配置Nginx文件
> https://www.digitalocean.com/community/tools/nginx?global.app.lang=zhCN


## Nginx 功能

- `url重写` 可根据域名、url、客户端的不同，转发http到不同的机器
- `静态资源压缩`
- 支持热部署、无需重启，更新配置文件
- 提供静态页面展示，网页服务
- 提供多个网站，多个域名的网页服务
- 提供反向代理服务
- 提供简单的资源下载服务
- 用户行为分析（日志功能）