1.PEP8 模块的导入顺序

```
系统 > 第三方 > 自建
```
2.model设计
```
第一层：operation.model
第二层：users.model  organization.model courses.model
无关层：EmailVerifyRecord.model Banner.model
```

3.导入时间模块

```
from datetime import datetime
```

4.定义EmailVerifyRecord

```
code 验证码 CharField
email 邮箱 EmailField
send_type 发送状态 CharField choices
seng_time 发送时间 DateTimeField default=datetime.now

MeTa

#注意：此时datetime.now()会返回model修改时间
```

5.定义 Banner

```
title 标题 CharField 
image 图片 ImageField upload_to max_length
url 链接 UrlField max_length
index 顺序 IntegerField default
add_time 添加时间 DateTimeField default

MeTa
```
6.数据库同步

```
makemigrations
migrate
```


