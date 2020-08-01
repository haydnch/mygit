



记录在阿里云ECS实例CentOS7.6 中安装Mysql数据库的步骤。

# 1 删除MariaDB

Cent OS 7 的 yum 源中已经不再包含在 MySQL，而改用了 MariaDB。

## 1 查询Maria DB是否已经安装

```
rpm -qa | grep maria*
```

##  2 删除MariaDB

```
yum -y remove maria*
```

# 2 下载mysql yum包

进入 mysql 官方提供的 yum 包下载页面，地址为：**[](https://dev.mysql.com/downloads/repo/yum/)** ，页面如下，选择适合自己系统的 yum 包。

![yum](https://gitee.com/haydnch/myImage/raw/master/imgs/yum.PNG)

这里下载的是==mysql80-community-release-el7-3.noarch.rpm==

# 3 安装mysql yum包

```
rpm -ivh mysql80-community-release-el7-3.noarch.rpm
```

# 4 安装mysql

```
yum install -y mysql-community-server
```

# 5 启动mysql

```
# 启动mysql 
systemctl start mysqld.service

# 查询mysql状态
systemctl status mysqld.service

#查看mysql安装路径
whereis mysql
```

![image-20200801183444424](https://gitee.com/haydnch/myImage/raw/master/imgs/image-20200801183444424.png)

# 6 更改默认密码

安装后默认会生成一个复杂临时密码，保存在```/var/log/mysqld.log ```这个文件中，可以输入以下命令通过查找文件得到密码。

- **查找默认密码**

```
grep 'temporary password' /var/log/mysqld.log
```

![image-20200801184705295](https://gitee.com/haydnch/myImage/raw/master/imgs/image-20200801184705295.png)

然后我们根据这个密码进入数据库。

如果不更改密码的话，无法进行数据库操作。

![image-20200801185011118](https://gitee.com/haydnch/myImage/raw/master/imgs/image-20200801185011118.png)

- **通过以下命令更改密码**

```
alter user 'root'@'localhost' identified by 'your_password';
```

在这里我们不能设置像1234、root这种简单密码，因为数据库设置了密码强度规则。因此先设置一个包含大小写字母、数字等的复杂密码，能通过强度验证。

![image-20200801185740361](https://gitee.com/haydnch/myImage/raw/master/imgs/image-20200801185740361.png)

- **查看密码相关安全设置**

![image-20200801185933120](https://gitee.com/haydnch/myImage/raw/master/imgs/image-20200801185933120.png)

- **修改密码强度设置**

  ```
  mysql> set global validate_password.length = 1;
  Query OK, 0 rows affected (0.01 sec)
  
  mysql> set global validate_password.policy = 0;
  Query OK, 0 rows affected (0.00 sec)
  ```

  设置以后就可以将数据库密码修改成简单密码了。

  当然，这个修改只建议在开发测试环境下使用，如果在生产环境使用简单密码，会导致数据库密码极易被破解，使得数据库中的数据有泄露的风险。

  # 7 设置允许远程连接

  由于是在阿里云ECS中安装的数据库，为了便于操作，我们通常在本地的数据库管理软件进行远程连接。

  首先在阿里云控制台安全组中添加配置规则，放行端口号3306。

  ![group](https://gitee.com/haydnch/myImage/raw/master/imgs/group.png)

  此时连接服务器上的数据库，会报错拒绝访问。

  ![deny](https://gitee.com/haydnch/myImage/raw/master/imgs/deny.png)

  回到服务器，查看用户表：

  ![image-20200801191820053](https://gitee.com/haydnch/myImage/raw/master/imgs/image-20200801191820053.png)

  用户root对应的host为localhost，只允许本地访问。因此执行以下命令：

  ```
  update user set host='%' where user='root';
  alter user 'root'@'%' identified with mysql_native_password by 'your_password';
  flush privileges;
  ```

  此时再在本地连接数据库，就可以连接成功。

  ![image-20200801192323522](https://gitee.com/haydnch/myImage/raw/master/imgs/image-20200801192323522.png)

  
  
  