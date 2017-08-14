1.安装xadmin

2.setting中引入app:xadmin, crispy_forms

3.admin中删除之前注册的model

```
注意,此时虽然我们删除了UserProfile,但是xadmin仍然会发现它,并将它注册到后台
```

4.urls中插入xadmin,修改xadmin.site.url

5.xadmin安装成功后,会存在一些默认的表,我们对xadmin进行数据库同步

```
存在三张表:
bookmark, usersettings, userwidget

makemigrations
migrate
```

6.我们通过git下载xadmin,我们将解压后的xadmin文件夹,复制到项目根目录之下

7.我们建立extra_apps package目录,通过它管理第三方插件包,然后我们拖入admin,并mark source root

8.此时我们可以通过项目引用xadmin,我们卸载admin

9.我们打开后台,发现界面有所改变(不一定一直有改变,只是源码此时比较新,还没有通过pypi发布)

10.不出意外,人家没出错,我又报错了,少模块,装呗

```
future   看介绍是用于python3支持python2的
six      这名字真特么清新脱俗,怎么想的都
```

11.我们在各个admin类同级别中新建adminx.py,然后对各个model进行注册

```
import xadmin

from .models import EmailVerifyRecord


class EmailVerifyRecordAdmin(object):
    pass

xadmin.site.register(EmailVerifyRecord, EmailVerifyRecordAdmin)
```
12.关于verbose_name_plural

```
是verbose_name的复数形式,不添加后,后台模块名称会加上s
```
13.我们在邮箱模块下进行添加操作,可能会出错

```
出错原因,因为我们卸载了系统中的xadmin之前进行了makemigrations,如果我们用源码进行了makemigrations,则会比原数据库增加一张xamdin_lob表
```
14.在同步的时候,会提示找不到xadmin

```
我们在setting.py中增加extra_app目录,想app目录一样
```

15.重载email类的unicode方法,后台界面在做类string的时候,会调用这个方法,不然会显示object的字符串,基本上都需要重载,尤其是作为其他字段的主键的时候,不重载大家都显示object字符串

```
    def __unicode__(self):
        return '{0}({1})'.format(self.code, self.email)
```
16.自定义显示列,可以使用数组,可以使用元祖,但是后者在队列中只有一个数据的时候,必须加上逗号

```
#在adminx.py中

class EmailVerifyRecordAdmin(object):
    list_display = ['code', 'email', 'send_type', 'send_time']
```
17.定义搜索和过滤器,注意,我们通常不对model中的数据进行实践搜索,但是可以在过滤器中进行时间搜索

```
class EmailVerifyRecordAdmin(object):
    list_display = ['code', 'email', 'send_type', 'send_time']
    search_fields = ['code', 'email', 'send_type']
    list_filter = ['code', 'email', 'send_type', 'send_time']
```

18.后续疯狂添加,发现一个bug

```
在定义了MeTa信息的时候,verbose_name被错误添加了u''信息,此时是不需要u''前缀的,在我改回来后,后台并不会生效,除非删掉重来添加
```





















