1.后台管理系统特点

```
权限管理

少前端样式

快速开发
```

2.setting文件自带app分析

```
django.contrib.admin        ------> admin.site.urls
django.contrib.auth
django.contrib.contenttypes    
django.contrib.sessions
django.contrib.messages
django.contrib.staticfiles

```

3.createsuperuser报错

```
#报错(查明应该是自定义长度和数据本身不符,来源于gender default=5  but (famale 女)
data too long for column

我们猜想是因为 sql-mode=”STRICT_TRANS_TABLES,NO_AUTO_Create_USER,NO_ENGINE "中的stric_trans_tables去掉，关闭严格模式，重启数据库

完成修改厚我们要再次进行数据库同步

#报错:和第一个报错原因一致,我们进行了错误的修改
Warning: Data truncated for column 'gender' at row 1
return self.cursor.execute(query, args)

#修改后同步,可能报错,也可能不报错

too many values to unpack

报错原因:合并app之前进行的数据库同步,合并app之后,数据库会自动添加(apps.)到外键之前,此时同步某个单一app时,apps.仍然存在,比较麻烦,要进行全局搜索进行删除

不抱错原因:合并app之后,进行数据库同步,推荐此种方法


```

4.更改中文

```
LANGUAGE_CODE = 'zh-hans'    

TIME_ZONE = 'Asia/Shanghai'

USE_TZ = False      #关闭utc时区

```

5.注册model并为model定义管理器

```
from .models import UserProfile


class UserProfileAdmin(admin.ModelAdmin):
    pass

admin.site.register(UserProfile, UserProfileAdmin)

```
