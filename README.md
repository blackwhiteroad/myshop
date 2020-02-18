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



