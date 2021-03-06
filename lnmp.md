### 安装nginx
- yum install nginx

### 安装mysql
1. 安装 yum 源
   - `wget https://dev.mysql.com/get/mysql57-community-release-el7-11.noarch.rpm`
   - `yum localinstall mysql57-community-release-el7-11.noarch.rpm`
2. 检测是否成功
   - `yum repolist enabled | grep "mysql.*-community.*"`
   - `yum install -y mysql-community-server`

3. 启动
   - `systemctl start mysqld`
4. 查看运行状态
   - `systemctl status mysqld`

5. 设置开机启动
   - `systemctl enable mysqld`
   - `systemctl daemon-reload`

6. 修改mysql root密码
   - `grep 'temporary password' /var/log/mysqld.log`
   - `mysql -uroot -p`
   - `ALTER USER 'root'@'localhost' IDENTIFIED BY 'MyNewPass4!';`  
或者
   - `set password for 'root'@'localhost'=password('MyNewPass4!'); `

7. 默认配置文件

   - 配置文件：/etc/my.cnf
   - 日志文件：/var/log/var/log/mysqld.log
   - 服务启动脚本：/usr/lib/systemd/system/mysqld.service
   - socket文件：/var/run/mysqld/mysqld.pid


### 安装php
- `rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm`
- `rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm`
- `yum search php71w`
- `yum install php71w php71w-fpm php71w-cli php71w-common php71w-devel php71w-gd php71w-pdo php71w-mysql php71w-mbstring php71w-bcmath php71w-pecl-redis`
- `service php-fpm start`
- `service nginx restart`

### 定时任务
```
*/5 * * * * /usr/bin/php /usr/www/test/gm/yii test/test >> /usr/logs/test_Error.log 2>&1
* * * * * /usr/bin/php /usr/www/test/gm/yii test/test >> /usr/logs/test_deduction_Error.log 2>&1
```
