1.user 同级生成course app，setting中注册
```
第一层：course.model
第二层：lesson.model video.model courseresource
```

2.Course.model  课程

```
name  课程名字charfield  
desc  课程描述charfield
detail 课程详情textfield
degree 课程等级charfield choices max_length/default
learn_times 学习时长 integerfield default=0   #不懂
students 学习人数 integerfield default
fav_nums 收藏人数 integerfield default
iamge 图片 imagefield upload_to
click_nums 点击数 integerfield default
add_time 添加时间 datetimefield default=datetime.now

MeTa

```

3.lesson
**注意外键的连接方式**

```
course = models.ForeignKey(Course, verbose_name=u'课程')     
name = models.CharField(max_length=100, verbose_name=u'章节')
add_time = models.DateTimeField(default=datetime.now, verbose_name='添加时间')

class MeTa:
    verbose_name = u'课程章节'
    verbose_name_plural = verbose_name

```

4.video

```
lesson = models.ForeignKey(Lesson, verbose_name=u'章节')
name = models.CharField(max_length=100, verbose_name=u'视频名称')
add_time = models.DateTimeField(default=datetime.now, verbose_name='添加时间')

class MeTa:
    verbose_name = u'视频'
    verbose_name_plural = verbose_name

```

5.courseresource

**新类型download文件**
```
course = models.ForeignKey(Course, verbose_name=u'课程')
name = models.CharField(max_length=100, verbose_name=u'课程资源')
add_time = models.DateTimeField(default=datetime.now, verbose_name='添加时间')
download = models.FileField(upload_to='course/resource/%Y/%m', verbose_name=u'资源文件', max_length=100 )                        

class MeTa:
    verbose_name = u'课程资源'
    verbose_name_plural = verbose_name


```