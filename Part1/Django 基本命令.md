# 基本命令

1. 开始一个django project
   django-admin startproject project_name
2. 新建一个django app
   ```python
   进入project目录:cd project_name
   python manage.py startapp app_name
   注意：django项目至少要包含一个应用
   ```

3. 创建models并同步数据库
   ```python
   # 生成数据库同步文件
   python manage.py makemigrations
   # 同步数据库
   python manage.py migrate
   ```

4. 启动服务

   ```python
   # 端口号可更改，默认8000
   python manage.py runserver 8000
   # 其他电脑也可访问
   python manage.py runserver 0.0.0.0:8000
   ```

5. 创建超级管理员

   ```python
   # 邮箱可以为空
   python manage.py createsuperuser
   # 修改密码 
   python manage.py changepassword username
   ```

6. 数据导入导出

   ```python
   python manage.py dumpdata appname > appname.json
   python manage.py loaddata appname.json
   ```

7. 终端相关

   ```python
   # 项目终端
   python manage.py shell
   # 数据库终端
   python manage.py dbshell
   ```
8. 其他命令
   ```python
   # 检查django项目完整性
   python manage.py check
   #查看数据库同步的sql语句
   python manage.py sqlmigrate

   更多执行python manage.py查看
   ```