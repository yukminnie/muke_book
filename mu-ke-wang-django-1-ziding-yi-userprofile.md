1.新建虚拟环境，创建项目

2.新建数据库，安装python-mysql，设置数据库连接，同步

3.设置utf8编码

4.设计model，编写用户表集成于系统User表

```
from django.contrib.auth.models import AbstractUser





昵称 性别 地址 手机： CharField，需要设置max_length

生日，头像：DataField,ImageField

手机，生日：可为空

性别，图片，地址：要有默认值，性别有choices，图片有upload_to,地址默认u''

特殊：图片也需要设置max_length



编写MeTa方法

编写__unicode__方法


```
5.ImageField属性依赖pillow库，我们通过IDE安装


6.重载user_model（setting.py）

```
AUTH_USER_MODEL = 'users.UserProfile'     重载UserProfile方法

```
7.数据库同步

```
makemigrations
migrate
```
8.至此，UserPorfile替换User成功