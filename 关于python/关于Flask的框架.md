# 关于Flask的框架

#### 第五章：数据库

首先需要安装两个flask插件，分别是`flask-SQLAlchemy`与`flask-migrate`，两个插件都需要在flask里初始化，~~或者说"注册"更好一些，我不是很清楚个中区别。~~首先需要初始化`flask-SQLAlchemy`，然后使用初始化后的实例与app本身初始化`flask-migrate`。

然后是`app/model.py`这个文件，这里面存放的是数据库的各个表单的抽象。在这个文件里：

1. **之后用到的所用包，除了flask的插件，似乎都是自带的，不需要额外下载，至少我是这样。**
2. 需要由`flask-SQLAlchemy`提供的基类来定义各个表单，同时还会用到`flask-SQLAlchemy`里提供的数据库字段类型，所以首先需要导入初始化后的`flask-SQLAlchemy`实例，也就是`form app import db`。
3. 对于用户表单，需要其实现登录功能，所以需要`flask-login`插件来管理用户登录状态，初始化该插件为`login`并导入，也就是`form app import login`。
4. 对于用户表单，要实现其登录功能，所以需要验证密码是否正确，这里使用的是`werkzeug.security`提供的`generate_password_hash`与`check_password_hash`两个函数，所以需要`from werkzeug.security import generate_password_hash, check_password_hash`。
5. 为了能够让`flask-login`访问到我们的`User`数据库字段(flask-login是一个插件，本身应该没有权利访问本地的数据库)，需要让`User`集成来自`flask-login`的`UserMixin`，所以需要`from flask-login import UserMixin`。
6. Post表单可以实现按照时间戳对用户动态进行排序，所以需要一个能够返回时间的函数，`from datetime import datetime`。
7. **非重点。**作者使用的头像服务需要根据用户的邮箱生成md5值，所以`from hashlib import md5`

关于数据库表单与表单之间的联系，以一对多来说，在"多"的这一方需要定义类似

```python
posts = db.relationship('Post', backref='author', lazy='dynamic')
```

在"一"的一方，需要定义一个外键指向"多"的一方，

```python
# flask-SQLAlchemy似乎自动把表单名转化为小写，在定义外键的时候
user_id = db.Column(db.Integer, db.foreignKey('user.id'))
```



