---
abbrlink: ''
categories:
- - 运维
- - 学习笔记
cover: https://s11.ax1x.com/2023/12/27/pibqs3T.jpg
date: '2023-11-13T14:54:40.051833+08:00'
recommend: '9999'
sticky: true
swiper: ''
tags:
- Hexo
- Qexo
title: 如何让部署Qexo后台
top: true
updated: 2024-1-2T21:8:21.754+8:0
---
现在 Qexo 官网拉下最新的代码 [跳转](https://github.com/Qexo/Qexo/releases)

然后解压

```
tar -xzf 文件名.tar.gz
```

#### 首先查看 Python 和 pip3 的版本，如果不对应最好安装如图中的版本不容易出错

![python和pip3版本](/img/py_v.png)

### 编辑配置

以使用 Mysql 为例, 确认好安装相关依赖后在`manage.py`的同级目录下创建并修改 `configs.py`

```python
import pymysql
pymysql.install_as_MySQLdb()
DOMAINS = ["127.0.0.1", "yoursite.com"]
DATABASES = {
    'default': {
            'ENGINE': 'django.db.backends.mysql',
            'NAME': 'qexo',
            'USER': 'root',
            'PASSWORD': 'password',
            'HOST': '127.0.0.1',
            'PORT': '3306',
            'OPTIONS': {
                "init_command": "SET sql_mode='STRICT_TRANS_TABLES'"
            }
    }
}

```

NAME 是数据库的名字；USER 是数据库的用户

然后在项目根目录依次执行如下

```cmd
pip3 install -r requirements.txt
python3 manage.py makemigrations
python3 manage.py migrate
python3 manage.py runserver 0.0.0.0:8000 --noreload
```

##### 如果`pip3 install -r requirements.txt` 时报错了，查看此文件夹，替换如下 requirements.txt

```cmd
Django==3.2.18
PyMySQL
boto3
requests
PyGithub
python-gitlab
html2text
PyYAML
urllib3
Markdown
djongo
django-cors-headers
pymongo
dnspython
sqlparse
psycopg2-binary
cryptography
pyopenssl
oss2
beautifulsoup4
```

最后在 ip 下加 8000 端口查看能否进入项目

如果没问题 就先关闭 下面是常驻项目进程命令

#### 常驻项目进程

`nohup python3 manage.py runserver 0.0.0.0:8000 --noreload`

输入完没报错就成功了 然后直接关闭这个 cmd 窗口不要`ctrl+c`

然后在你服务器 ip 加让 8000 端口就可以访问了

### 停止进程

如果你想关闭这个常驻进程 需要查询 8000 端口然后杀掉这个进程

#### Linux

`lsof -i :8000`

根据上一步的输出，找到占用 8000 端口的进程的 PID（进程 ID）

使用 `kill` 命令终止该进程。将 `<PID>` 替换为实际的进程 ID

`kill <PID>`

#### AMH

`netstat -tlnp | grep 8000`

`kill <PID>`
