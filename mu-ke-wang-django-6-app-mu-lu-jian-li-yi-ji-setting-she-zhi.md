1.将建立的app加入到新的apps package文件夹中,此时会报引用错误

```
search for references    搜索相关引用   去除

open moved files in eitor    打开移动的文件   去除
```

2.将apps目录mark as sources root,此时IDE不会报错,但是外部命令行runserver会报错,我们引入settings设置

```
注意apps合并厚,并没有进行数据库同步操作

```
3.settings设置,将apps设置为根目录第一顺位,此时外部命令行runserver正常

```
import sys

sys.path.insert(0, os.path.join(BASE_DIR, 'apps'))
```

4.debeg