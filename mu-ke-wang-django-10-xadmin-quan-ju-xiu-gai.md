1.开启主题,此时主题没有生效,猜测是因为使用了本地xadmin的缘故

```
from xadmin import views

class BaseSetting(object):
    enable_themes = True
    use_bootswatch = True
    
xadmin.site.register(views.BaseAdminView, BaseSetting)
```

2.全局样式修改

```

from xadmin import views

class GlobalSettings(object):
    site_title = "慕学后台管理系统"  # 系统名称
    site_footer = "慕学在线网"      # 底部版权栏
# menu_style = "accordion"    

xadmin.site.register(views.CommAdminView, GlobalSettings)

```


3.导航栏菜单修改,所有app都需要修改

在app文件中,添加verbose_name信息,注意声明编码
```
#!user/bin/python
# _*_ coding: utf-8 _*_

verbose_name = u'课程信息'
```
在init文件中,修改默认default_app_config
```
default_app_config = 'courses.apps.CoursesConfig'
```