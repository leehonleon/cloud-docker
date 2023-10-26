# 微服务开发环境 Docker

本项目是 [微服务开发环境](https://github.com/leehonleon/cloud-docker) Server 的 docker Compose 启动环境,以及 Nacos server 在 docker 的单机和集群的运行例子.

## 注意

本脚本默认使用了 Nacos v1.4.6 版本，启动其他版本请修改.env 文件。

- NACOS_VERSION=v1.4.6 #规定启动 nacos 版本号
- PRJNAME=cloud #设置启动的容器名前缀

脚本库中有很多冗余文件，原因是本仓库 copy 自[Nacos-group](https://github.com/nacos-group/nacos-docker.git),该项目中可以配置 nacos 集群服务等任务。为了以后本项目也可以拓展，所以暂时留下。

## 项目目录

- env: docker compose 环境变量文件
- cloud-dev: docker-compose 编排例子

## 运行环境

- [Docker](https://www.docker.com/)

### 注意事项

- 从 Nacos 最新版本为 nacos:nacos-server/latest
- 从 Nacos 1.3.1 版本开始,数据库存储已经升级到 8.0, 并且它向下兼容
- 例子演示中使用的数据库是为了方便定制了官方 Mysql 镜像, 自动初始化的数据库脚本.
- 如果你使用自定义数据库,
  第一次启动 Nacos 前需要手动初始化 [数据库脚本](https://github.com/alibaba/nacos/blob/master/distribution/conf/mysql-schema.sql)

## 快速开始

打开命令窗口执行：

- Clone project

  ```powershell
  git clone --depth 1 https://github.com/leehonleon/cloud-docker.git
  cd cloud-docker
  ```

  ```powershell
  # Using mysql 5.7
  docker-compose -f cloud-dev/standalone-mysql-5.7.yaml up
  ```

  想要启动后台模式,请在上述命令后面增加 -d

## 检查

- 检查数据库，端口为 3306，密码在 env/mysql.env 文件中

- 检查 nacos 访问 [http://localhost:8848/nacos/index.html]

- 检查 Rabbit 与初次设置.
  [http://localhost:15672/]
  使用账户 guest/guest 登录, 添加账户并设置访问权限.

- 检查 redis. 端口为 6379, 账户名在 ./env/redis.conf 中 requirepass 的设定

## 参考

- nacos 的配置说明,可以参看[NACOS](README_NACOS.md)

- RabbitMQ 的配置说明,参看[RabbitMQ](README_RABBITMQ.md)
