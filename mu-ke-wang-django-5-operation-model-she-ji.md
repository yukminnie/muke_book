1.建立app，加入app，设置编码,import datetime

2.代码

```
class UserAsk(models.Model):
    name = models.CharField(max_length=20, verbose_name=u'姓名')
    mobile = models.CharField(max_length=11, verbose_name=u'手机')
    course_name = models.CharField(max_length=50, verbose_name=u'课程名')
    add_time = models.DateTimeField(default=datetime.now, verbose_name=u'咨询时间')

    class MeTa:
        verbose_name = u'用户咨询'
        verbose_name_plural = verbose_name


class CourseComments(models.Model):
    course = models.ForeignKey(Course, verbose_name=u'课程')
    user = models.ForeignKey(UserProfile, verbose_name=u'用户')
    comments = models.CharField(max_length=200, verbose_name=u'评论')
    add_time = models.DateTimeField(default=datetime.now, verbose_name=u'添加时间')

    class MeTa:
        verbose_name = u'课程评论'
        verbose_name_plural = verbose_name


class UserFavorite(models.Model):
    user = models.ForeignKey(UserProfile, verbose_name=u'用户')
    fav_id = models.IntegerField(default=0, verbose_name=u'数据id')
    fav_type = models.IntegerField(default=1, choices=(
        (1, '课程'),
        (2, '课程机构'),
        (3, '教师')
    ), verbose_name='收藏类型')
    add_time = models.DateTimeField(default=datetime.now, verbose_name=u'添加时间')

    class MeTa:
        verbose_name = u'用户收藏'
        verbose_name_plural = verbose_name


# 没有使用外键，区分系统消息和用户消息
class UserMessage(models.Model):
    user = models.IntegerField(default=0, verbose_name=u'接收用户')
    message = models.CharField(max_length=500, verbose_name=u'消息内容')
    has_read = models.BooleanField(default=False, verbose_name=u'是否已读')
    add_time = models.DateTimeField(default=datetime.now, verbose_name=u'添加时间')

    class MeTa:
        verbose_name = u'用户消息'
        verbose_name_plural = verbose_name


class UserCourse(models.Model):
    course = models.ForeignKey(Course, verbose_name=u'课程')
    user = models.ForeignKey(UserProfile, verbose_name=u'用户')
    add_time = models.DateTimeField(default=datetime.now, verbose_name=u'添加时间')

    class MeTa:
        verbose_name = u'用户课程'
        verbose_name_plural = verbose_name
```
3.同步

```
makemigrations
migrate
```