# SQLAlchemy

SQLAlchemy is an Object-Relational Mapping (ORM) library for Python.

It provides a set of high-level APIs to interact with databases in an object-oriented manner.

It allows to map Python objects to database tables and perform SQL operations with ease.

## Setting up SQLAlchemy

Install SQLAlchemy:

```bash
pip install sqlalchemy
```

## Setting up SQLAlchemy in a project

Once installed, configure SQLAlchemy by setting up the connection to the database:

```python
from sqlalchemy import create_engine
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy.orm import sessionmaker

# Create a database engine
engine = create_engine('sqlite:///example.db')

# Create a base class for declarative models
Base = declarative_base()

# Create a session factory
Session = sessionmaker(bind=engine)
session = Session()
```

## Defining models and creating the database schema

Define the models as Python classes that inherit from Base.

Example:

```python
from sqlalchemy import Column, Integer, String, create_engine
from sqlalchemy.ext.declarative import declarative_base

Base = declarative_base()

class User(Base):
    __tablename__ = 'users'
    id = Column(Integer, primary_key=True)
    name = Column(String)
    age = Column(Integer)

# Create all tables in the database
Base.metadata.create_all(engine)
```

## CRUD operations with SQLAlchemy

SQLAlchemy simplifies CRUD operations.

Example of Create:

```python
new_user = User(name='Daniel', age=24)
session.add(new_user)
session.commit()
```

Example of Read:

```python
user = session.query(User).filter_by(name='Daniel').first()
```

Example of Update:

```python
user.age = 25
session.commit()
```

Example of Delete:

```python
session.delete(user)
session.commit()
```

## Relationship management

### One-to-many relationship

```python
class Post(Base):
    __tablename__ = 'posts'
    id = Column(Integer, primary_key=True)
    title = Column(String)
    user_id = Column(Integer, ForeignKey('users.id'))
    
    user = relationship('User', back_populates='posts')

class User(Base):
    __tablename__ = 'users'
    id = Column(Integer, primary_key=True)
    name = Column(String)
    
    posts = relationship('Post', back_populates='user')
```

### Many-to-many relationship

```python
post_tags = Table('post_tags', Base.metadata,
    Column('post_id', Integer, ForeignKey('posts.id')),
    Column('tag_id', Integer, ForeignKey('tags.id'))
)

class Post(Base):
    __tablename__ = 'posts'
    id = Column(Integer, primary_key=True)
    title = Column(String)
    tags = relationship('Tag', secondary=post_tags)

class Tag(Base):
    __tablename__ = 'tags'
    id = Column(Integer, primary_key=True)
    name = Column(String)
```

## Advanced queries and joins

### Inner Join

```python
from sqlalchemy.orm import aliased

user = aliased(User)
post = aliased(Post)

all = session.query(user, post).join(post, post.user_id == user.id).all()

filtered = session.query(Post).filter(Post.title.like('%\Flask%')).all()
```

### Left Outer Join

```python
query = session.query(User, Post).outerjoin(Post, Post.user_id == User.id).all()

for user, post in query:
    print(f'User: {user.name}, Post: {post.title if post else "No Post"}')
```

### Join with Aliases

```python
from sqlalchemy.orm import aliased

user_alias = aliased(User)
post_alias = aliased(Post)

query = session.query(user_alias, post_alias).join(post_alias, post_alias.user_id == user_alias.id).all()

for user, post in query:
    print(f'User: {user.name}, Post: {post.title}')
```

### Union

```python
query1 = session.query(User.name).filter(User.age > 18)

query2 = session.query(Post.title).filter(Post.title.like('%\Flask%'))

union_query = query1.union(query2).all()

for result in union_query:
    print(result)
```

## SQLAlchemy ORM vs Core

SQLAlchemy offers two main ways to interact with databases.

### ORM

Allows to define models as Python classes and interact with them as objects.

It abstracts away SQL queries and makes working with databases more intuitive.

Most operations are done using the session object.

```python
user = session.query(User).filter_by(name='Daniel').first()
```

### Core

Provides an explicit approach with the database using SQL expressions and queries.

This approach does not rely on ORM models but directly constructs SQL statements.

```python
from sqlalchemy import select, table, column
users = table('users', column('name'))
query = select([users]).where(users.c.name == 'John')
result = engine.execute(query)
```