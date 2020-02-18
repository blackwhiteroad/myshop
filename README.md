## myshop
购物项目

### 说明
此文档用于配置项目的详细指导说明

#### 配置win10项目环境
##### 关于win10，配置virtualenvwrapper
https://blog.csdn.net/pzl_pzl/article/details/80745039

如下是配置虚拟环境跟安装项目依赖包
```
mkvirtualenv vueShop
pip install -i https://pypi.douban.oom/simple djangorestframework django-filter markdown
pip install mysqlclient pillow  # pillow处理图片
注:当pip install xxx命令无效时，在此https://www.lfd.uci.edu/~gohlke/pythonlibs下载安装包/模块
```
使用专业版pycharm新建django项目，解释器指定为虚拟环境的python

##### 补充:关于linux
Ⅰ. 安装并配置
```
pip install virtualenv virtualenvwrapper    # pip install -i https://pypi.douban.com/simple virtualenv virtualenvwrapper    ## 使用豆瓣加速源
mkdir /root/.envs
cat >> /etc/profile <<EOF
export WORKON_HOME=/root/.Envs          # 创建存放虚拟环境的路径
source /usr/bin/virtualenvwrapper.sh    # which virtualenvwrapper.sh查看安装路径
EOF
source /etc/profile
```
注:未能生效，请重新登入

Ⅱ. 使用
1. 创建虚拟环境
> mkvirtualenv -p python3 nature

2. 查看虚拟环境
> workon     
or
> lsvirtualenv

3. 进入虚拟环境
> worken nature

4. 推出虚拟环境
> deactivate

5. 删除虚拟环境
> rmvirtualenv nature   

#### win10配置本地mysql8数据库
cmd管理员命令行操作
```
choco install mysql
# -----修改root密码及访问密码方式，并授权所有主机可以连接-----
## ---修改root密码---
net stop mysql
mysqld --console --skip-grant-tables --shared-memory 
### 新开命令行
mysql -uroot -p
mysql> update mysql.user set authentication_string='' where user='root';
mysql> quit
### 关闭mysqld --console --skip-grant-tables --shared-memory命令行界面
net start mysql
mysql -u root -p
mysql> alter mysql.usere 'root'@'localhost' identified by '123456';
mysql> quit
## -----------------

## ---设置所有主机可以访问---
注:navicat连接数据库报错信息-->1130 - host 'desktop-opdnhse' is allowed to connect to this mysql server
mysql> select Host,User from mysql.user;   # 查看Host的访问形式
+-----------+------------------+
| Host      | User             |
+-----------+------------------+
| localhost | mysql.infoschema |
| localhost | mysql.session    |
| localhost | mysql.sys        |
| localhost | root             |    # localhost 需要改为%
+-----------+------------------+
mysql> update mysql.user set `Host` = '%' where `Host` = 'localhost' and User = 'root';
mysql> flush privileges;
mysql> grant all privileges on *.* to 'root'@'%' identified by '123456' with grant option;
mysql> flush privileges;
## ------------------------

## ---修改访问密码方式---
注:由于使用的是navicate1.11版本，使用的连接密码方式为mysql_native_password，而mysql8为caching_sha2_password，故需要更改
mysql> select Host,User,Plugin from mysql.user;
+-----------+------------------+-----------------------+
| Host      | User             | Plugin                |
+-----------+------------------+-----------------------+
| %         | root             | caching_sha2_password |
| localhost | mysql.infoschema | caching_sha2_password |
| localhost | mysql.session    | caching_sha2_password |
| localhost | mysql.sys        | caching_sha2_password |
+-----------+------------------+-----------------------+
mysql> ALTER USER 'root'@'%' IDENTIFIED BY 'root' PASSWORD EXPIRE NEVER;
mysql> ALTER USER 'root'@'%' IDENTIFIED BY 'root' PASSWORD EXPIRE NEVER;
## ---------------------
```

