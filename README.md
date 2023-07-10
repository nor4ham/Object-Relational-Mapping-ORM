# ObjectRelationalMapping

### What is an ORM?
ORM, or Object-Relational Mapping, is a technique used to bridge the gap between object-oriented programming and relational databases. It allows you to interact with the database using objects and their relationships, rather than writing raw SQL queries.
In Python, there are several ORM libraries available, and one of the most popular ones is SQLAlchemy. Let's dive into an example using SQLAlchemy:
1.    <b>Installation </b>:
Before you can use SQLAlchemy, you need to install it. You can install it using pip by running the following command:
```
pip install SQLAlchemy

```
2.  <b> Setting up the Database: </b>
In this example, we'll use an SQLite database. First, import SQLAlchemy and create an engine that will handle the connection to the database:
```
from sqlalchemy import create_engine
engine = create_engine('sqlite:///example.db')
```
3. <b> Creating a Model: </b>
Next, define a Python class that represents a table in the database. Each instance of the class will correspond to a row in the table. SQLAlchemy provides a base class called declarative_base() that you can use as a parent class for your models:
```
from sqlalchemy import Column, Integer, String
from sqlalchemy.ext.declarative import declarative_base

Base = declarative_base()

class User(Base):
    __tablename__ = 'users'

    id = Column(Integer, primary_key=True)
    name = Column(String)
    email = Column(String)

```
4. <b> Interacting with the Database: </b>
Once you have your model defined, you can perform various database operations such as inserting, querying, updating, and deleting records. Here's an example of using the model:
```
from sqlalchemy.orm import sessionmaker

# Create a session factory bound to the engine
Session = sessionmaker(bind=engine)
session = Session()

# Insert a new user
new_user = User(name='John Doe', email='john@example.com')
session.add(new_user)
session.commit()

# Query all users
users = session.query(User).all()
for user in users:
    print(user.name, user.email)

# Update a user
user = session.query(User).filter_by(name='John Doe').first()
user.email = 'johndoe@example.com'
session.commit()

# Delete a user
user = session.query(User).filter_by(name='John Doe').first()
session.delete(user)
session.commit()

```
In the above example, we create a session using the sessionmaker class, which represents a transaction with the database. We can then use this session to add new records, query existing records, update records, or delete records.

By defining the model using classes and attributes, SQLAlchemy handles the translation between the object-oriented model and the relational database, allowing you to interact with the database using Python objects and methods.

This is a basic example of using ORM with SQLAlchemy in Python. Keep in mind that SQLAlchemy provides many advanced features, such as relationships between tables, complex queries, and more.







# Resources
https://betterprogramming.pub/building-the-rust-web-app-how-to-use-object-relational-mapper-3af2084555b6
https://blog.bitsrc.io/what-is-an-orm-and-why-you-should-use-it-b2b6f75f5e2a
