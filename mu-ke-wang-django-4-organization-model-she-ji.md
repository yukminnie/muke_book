1.建立app，加入app，设置编码,import datetime

2.层级关系
```
第一层：citydict
第二层：course_org
第三层：teacher
```

3.代码

```
class CityDict(models.Model):
    name = models.CharField(max_length=20, verbose_name=u'城市名')
    add_time = models.DateTimeField(default=datetime.now)
    desc = models.CharField(max_length=200, verbose_name=u'机构描述')

    class MeTa:
        verbose_name = u'所在城市'
        verbose_name_plural = verbose_name


# Create your models here.
class CourseOrg(models.Model):
    name = models.CharField(max_length=50, verbose_name=u'机构名称')
    desc = models.TextField(verbose_name=u'机构描述')
    click_nums = models.IntegerField(default=0, verbose_name=u'点击数')
    fav_nums = models.IntegerField(default=0, verbose_name=u'点赞数')
    image = models.ImageField(upload_to='org/%Y/%m', max_length=100, verbose_name='封面图')
    address = models.CharField(max_length=150, verbose_name=u'机构地址')
    city = models.ForeignKey(CityDict, verbose_name=u'所在城市')
    add_time = models.DateTimeField(default=datetime.now)

    class MeTa:
        verbose_name = u'课程机构'
        verbose_name_plural = verbose_name


class Teacher(models.Model):
    org = models.ForeignKey(CourseOrg, verbose_name=u'所属机构')
    name = models.CharField(max_length=20, verbose_name=u'教师名')
    work_years = models.IntegerField(default=0, verbose_name=u'工作年限')
    work_company = models.CharField(max_length=50, verbose_name=u'就职公司')
    work_position = models.CharField(max_length=50, verbose_name=u'公司职位')
    points = models.CharField(max_length=50, verbose_name=u'教学特点')
    click_nums = models.IntegerField(default=0, verbose_name=u'点击数')
    fav_nums = models.IntegerField(default=0, verbose_name=u'点赞数')
    add_time = models.DateTimeField(default=datetime.now)

    class MeTa:
        verbose_name = u'教师'
        verbose_name_plural = verbose_name
```

4.数据库同步
```
makemigrations
migrate
```