
# DolphinScheduler升级文档

## 1. 备份上一版本文件和数据库

## 2. 停止dolphinscheduler所有服务

 `sh ./script/stop-all.sh`

## 3. 下载新版本的安装包

- [下载](https://dolphinscheduler.apache.org/zh-cn/download/download.html), 下载最新版本的二进制安装包
- 以下升级操作都需要在新版本的目录进行

## 4. 数据库升级

- **请先备份现有数据库**

- 修改conf/datasource.properties中的下列属性

- 如果选择 MySQL，请注释掉 PostgreSQL 相关配置(反之同理), 还需要手动添加 [[ mysql-connector-java 驱动 jar ](https://downloads.MySQL.com/archives/c-j/)] 包到 lib 目录下，这里下载的是mysql-connector-java-8.0.16.jar，然后正确配置数据库连接相关信息

    ```properties
      # postgre
      #spring.datasource.driver-class-name=org.postgresql.Driver
      #spring.datasource.url=jdbc:postgresql://localhost:5432/dolphinscheduler
      # mysql
      spring.datasource.driver-class-name=com.mysql.jdbc.Driver
      spring.datasource.url=jdbc:mysql://xxx:3306/dolphinscheduler?useUnicode=true&characterEncoding=UTF-8&allowMultiQueries=true     需要修改ip，本机localhost即可
      spring.datasource.username=xxx						需要修改为上面的{user}值
      spring.datasource.password=xxx						需要修改为上面的{password}值
    ```

- 执行数据库升级脚本

`sh ./script/create-dolphinscheduler.sh`

## 5. 服务升级

### 5.1 修改`conf/config/install_config.conf`配置内容
单机部署请参照[单机部署(Standalone)](./installation/standalone.md)中的`6.修改运行参数部分`
集群部署请参照[集群部署(Cluster)](./installation/standalone.md)中的`6.修改运行参数部分`

### 注意事项

1、修改conf/config/install_config.conf中的workers参数

假设以下为要部署的worker主机名和ip的对应关系
| 主机名 | ip |
| :---  | :---:  |
| ds1   | 192.168.xx.10     |
| ds2   | 192.168.xx.11     |
| ds3   | 192.168.xx.12     |

那么为了保持与之前版本worker分组一致，则需要把workers参数改为如下

```shell
#worker服务部署在哪台机器上,并指定此worker属于哪一个worker组
workers="ds1:service1,ds2:service2,ds3:service2"
```

### 5.2 执行部署脚本
```shell
`sh install.sh`
```


