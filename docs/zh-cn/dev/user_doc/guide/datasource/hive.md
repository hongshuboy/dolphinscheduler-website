# HIVE数据源

## 使用HiveServer2

 <p align="center">
    <img src="/img/hive_edit.png" width="80%" />
  </p>

- 数据源：选择HIVE
- 数据源名称：输入数据源的名称
- 描述：输入数据源的描述
- IP/主机名：输入连接HIVE的IP
- 端口：输入连接HIVE的端口
- 用户名：设置连接HIVE的用户名
- 密码：设置连接HIVE的密码
- 数据库名：输入连接HIVE的数据库名称
- Jdbc连接参数：用于HIVE连接的参数设置，以JSON形式填写

> 注意：如果您希望在同一个会话中执行多个 HIVE SQL，您可以修改配置文件 `common.properties` 中的配置，设置 `support.hive.oneSession = true`。
> 这对运行 HIVE SQL 前设置环境变量的场景会很有帮助。参数 `support.hive.oneSession` 默认值为 `false`，多条 SQL 将在不同的会话中运行。

## 使用HiveServer2 HA Zookeeper

 <p align="center">
    <img src="/img/hive_edit2.png" width="80%" />
  </p>


注意：如果没有开启kerberos,请保证参数 `hadoop.security.authentication.startup.state` 值为 `false`,
参数 `java.security.krb5.conf.path` 值为空. 开启了**kerberos**，则需要在 `common.properties` 配置以下参数

```conf
# whether to startup kerberos
hadoop.security.authentication.startup.state=true

# java.security.krb5.conf path
java.security.krb5.conf.path=/opt/krb5.conf

# login user from keytab username
login.user.keytab.username=hdfs-mycluster@ESZ.COM

# login user from keytab path
login.user.keytab.path=/opt/hdfs.headless.keytab
```

