# Nodejs

## 容灾

是指通过技术和管理手段，确保当应用系统或数据中心因灾难（如硬件故障、自然灾害、网络攻击）而中断时，能够迅速恢复业务运行并最大程度减少损失的能力

**解决方式**

#### 1.负载均衡与多实例部署

通过反向代理（如 Nginx）或负载均衡器（如 AWS ELB）分发流量到多个 Node.js 实例。如果一个实例发生故障，流量可自动转移到其他实例。

#### 2.数据库高可用

使用主从复制、读写分离。部署数据库集群（如 MongoDB Replica Set 或 MySQL 集群）以应对单点故障。

#### 3.自动重启与监控

使用进程管理工具（如 PM2）监控 Node.js 服务，崩溃时自动重启。配置 APM 工具（如 New Relic 或 Sentry）监控性能与错误。

#### 4.日志与备份

通过集中式日志系统（如 ELK 或 Loki）存储应用日志，快速分析问题。

#### 5.CDN 与缓存

将静态资源部署到 CDN，减少对后端服务的依赖。使用缓存（如 Redis）加速常用数据查询。

#### 6.区域容灾与异地部署

使用云服务的多区域部署功能（如 AWS Regions），确保区域故障不会影响全局服务。配置 DNS 轮询以实现跨区域流量切换。

#### 7. 健康检查与熔断

实现应用健康检查接口，定期检查服务状态。使用熔断器（如 opossum 库）处理下游服务故障。