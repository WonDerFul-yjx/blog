搭建django环境
1. 创建虚拟环境,并激活

```
virtualenv -p python3 venv
source venv/bin/activate
```

2. 通过pip安装django、mysqlclient

```
pip install django
pip install mysqlclient
```

注：安装mysqlclient如果报错【mysql_config not found】,请配置环境变量： [Mac OS 下安装mysqlclient报“mysql_config not found”的解决](https://www.cnblogs.com/njj10/p/7676123.html)

查看PATH变量
```
echo $PATH
```

3. 查看django的版本

方法1：
```
python -m django --version
```

方法2：
```
import django
print(django.get_version())
```

4. 创建一个项目(Project)：mysite
```
django-admin startproject mysite
```

5. 启动项目(默认端口8000）

```
python manage.py runserver
python manage.py runserver 8080
python manage.py runserver 0:8080
```
如果你想要修改服务器监听的IP，在端口之前输入新的。示例中0 即是 0.0.0.0的缩写

6. 创建一个应用(App)：
```
python manage.py startapp polls
```
将应用配置到settings中
```
...
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'polls.apps.PollsConfig',
]
...
```

7. 编写试图view
pools/view.py
```
fromm django.http import HttpResponse

def index(request):
    return HttpResonse("hello world.")
```
新建urls.py
```
from django.urls import path
from . impor views

urlpatterns = [
    path('', views.index, name='index'),
]
```
配置mysite/urls.py

```
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('polls/', include('pools.urls')),
    path('admin/', admin.site.urls),
]
```

第二部分：配置数据库
mysite/settings.py
```
...
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'HOST': 'xxx',
        'USER': 'xxx',
        'PASSWORD': 'xxx',
        'NAME': 'xxx',
    }
}
...
```
配置好数据库连接后，生成
```
python manage.py migrate
```

写模型

生成对应数据库
