---
title: "sqlalchemy"
date: "2021-06-16T11:11:38"
description: "Anki deck for sqlalchemy cards."
draft: true
# image: /path/to/image
css: custom-styles.css
---

# sqlalchemy


## How do you specify a one to many relationship in sqlalchemy?

1. Add a `relationship` field to the `one` table which references the `many` table.
2. Add a column to the `many` table which references the primary key of the `one` table with a `ForeignKey`

```python
from sqlalchemy.orm import relationship
from sqlalchemy import Column, Integer, ForeignKey

class One(Base):
    __tablename__ = 'one'
    id = Column(Integer, primary_key=True)
    many = relationship("Many")

class Many(Base):
    __tablename__ = 'many'
    id = Column(Integer, primary_key=True)
    one_id = Column(Integer, ForeignKey('one.id'))
```

## How do you create a one-to-one relationship in sqlalchemy?

Convert a `one-to-many` relationship to `one-to-one` by specifying `uselist=False` on the relationship in the many side of the relationship

```python
from sqlalchemy.orm import relationship
from sqlalchemy import Column, Integer, ForeignKey

class One(Base):
    __tablename__ = 'one'
    id = Column(Integer, primary_key=True)
    many_as_one_id = Column(Integer, ForeignKey('manyAsOne.id'))
    manyAsOne = relationship("Many", uselist=False)

class ManyAsOne(Base):
    __tablename__ = 'manyAsOne'
    id = Column(Integer, primary_key=True)
```

## What are the two ways of creating a bidirectional relationship in sqlalchemy?

1. Use the `backref` keyword argument on the table which has a foreign key
2. Add a `relationship` to both tables which references the other table and includes a `back_populates` keyword

## What is the difference between the `backref` and `back_populates` keywords in sqlalchemy `relationship`s?

The `backref` keyword automatically creates a property on the referenced class

The `back_populates` keyword references a property on the referenced class but that property must be manually specified as a `relationship`

*the following examples are equivalent"

```python
# back_populates
class One(Base):
    __tablename__ = 'one'
    id = Column(Integer, primary_key=True)
    many = relationship("Many", back_populates="one")

class Many(Base):
    __tablename__ = 'many'
    id = Column(Integer, primary_key=True)
    one_id = Column(Integer, ForeignKey('one.id'))
    one = relationship("One", back_populates="many")
```

```python
# back_ref
class One(Base):
    __tablename__ = 'one'
    id = Column(Integer, primary_key=True)
    many = relationship("Many", back_ref="one")

class Many(Base):
    __tablename__ = 'many'
    id = Column(Integer, primary_key=True)
    one_id = Column(Integer, ForeignKey('one.id'))
```

## How do you specify a many to many relationship in sqlalchemy?

1. Create an `association table` between two classes.
2. Add `secondary=association_table` to the relationships

```python
association_table = Table('association', Base.metadata,
    Column('left_id', Integer, ForeignKey('left.id')),
    Column('right_id', Integer, ForeignKey('right.id'))
)

class Parent(Base):
    __tablename__ = 'left'
    id = Column(Integer, primary_key=True)
    children = relationship(
        "Child",
        secondary=association_table,
        back_populates="parents")

class Child(Base):
    __tablename__ = 'right'
    id = Column(Integer, primary_key=True)
    parents = relationship(
        "Parent",
        secondary=association_table,
        back_populates="children")
```

## What is late evaluation of relationship arguments in sqlalchemy?

The evaluation of strings in relationships to python classes and columns is performed lazily.

The first argument of a `relationship` is a target class referenced by a string name rather than the class itself.

```python
class Parent(Base):
    # ...

    children = relationship("Child", back_populates="parent")

class Child(Base):
    # ...

    parent = relationship("Parent", back_populates="children")
```

## How do you specify a Foreign Key in sqlalchemy?

```python
Column('column_name', ColumnType, ForeignKey('foreign_table.foreign_column'))
```

```python
Column('user_id', Integer, ForeignKey('user.user_id'))
```

## How do you add an `ON UPDATE` constraint to a `ForeignKey` in sqlalchemy?

Use the `onupdate` keyword in the `ForeignKey`

```python
Column('user_id', Integer, ForeignKey('user.user_id', onupdate='CASCADE'))
```

## How do you add an `ON DELETE` constraint to a `ForeignKey` in sqlalchemy?

Use the `ondelete` keyword in the `ForeignKey`

```python
Column('user_id', Integer, ForeignKey('user.user_id', ondelete='CASCADE'))
```

## What is the difference between foreign key `ON DELETE` constraints and relationship `cascade="all, delete"` constraints in sqlalchemy?

The relationship `cascade` constraint will issue `DELETE` queries for all of the referenced items and will make sure that the proper items are deleted from the session. The foreign key constraint will cause items to be deleted in the database but sqlalchemy does not track the state of local objects based on the foreign key alone.

## How do you specify a unique constraint in sqlalchemy?

Use the `unique` keyword on a column.

```python
Column('user_id', Integer, unique=True)
```

## How do you specify a primary key constraint in sqlalchemy?

Use the `primary_key` keyword on a column.

```python
Column('user_id', Integer, primary_key=True)
```

## How do you create an index in sqlalchemy?

Use the `index` keyword on a column.

```python
Column('user_id', Integer, index=True)
```

## How can you pass both positional and keyword arguments to `__table_args__` in sqlalchemy?

Keyword arguments can be specified by making the last argument to a tuple of `__table_args__` a dictionary.


```python
class MyClass(Base):
    __tablename__ = 'sometable'
    __table_args__ = (
            ForeignKeyConstraint(['id'], ['remote_table.id']),
            UniqueConstraint('foo'),
            {'autoload':True}
            )
```
