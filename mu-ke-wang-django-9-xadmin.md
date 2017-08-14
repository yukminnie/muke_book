1.关于外键字段添加到adminx.py中的注意事项,过滤器字段的外键字段需要添加__name后缀

```
class LessonAdmin(object):
    list_display = ['course', 'name', 'add_time']
    list_filter = ['course__name', 'name', 'add_time']
    search_fields = ['course', 'name']

```
