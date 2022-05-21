---
layout: post
author: "0x4D5041"
title: Working with MongoDB & Python
icon: python
date: 2022-05-21 13:51 -03:00
modified: 
tags: [python]
description: Working with Pymongo module
---

<img src="../assets/img/working-with-mongodb-and-python/banner.png" alt="mongodb and python">

## Pymongo

[Pymongo](https://pymongo.readthedocs.io/en/stable/) is a module that allows us interact with [MongoDB](https://www.mongodb.com/) databases using Python.

To install it just type:
```bash
python3 -m pip install pymongo
```

## Starting mongod service

***You should have _mongod_ running on your host**

To start running mongod service type on the command line
```bash
user@xxxx:~$ mongod
```
It should create a new database on _/home/usr/data/db_ but
you can specify a diferent directory with the data folder

```bash
user@xxxx:~$ mongod --dbpath /path/to/folder
```

## Connecting
To interact with a Mongo database, pymongo requires import the _MongoClient_ to connect to server and start getting database info.

Connect to the server requires the hosts and port, if you are running localy, _mongod_ runs on **_localhost:27017_**

```python
>>> from pymongo import MongoClient
>>> 
>>> MONGO_URI = 'mongodb://localhost'
>>> client = MongoCLient(MONGO_URI)
```

Using the client, it's possible to connect and store data, also with their collections.
The collections are very similar to a SQL Table.



```python
>>> db = client['myStore']
>>> collections = db['products']
```
If the db does not exists, it'll be created.

## Inserting, finding and deleting data

### Inserting a document into a collection

```python
>>> collections.insert_one({
    '_id':1,
    'name': 'Tiro Track Pants',
    'color':'Black/White',
    'size':'XS'
    'price': 75
})
```

To insert many documents into the collection using one line

```python
>>> product_one = {
    'name':'Hoodie', 'color':'Red/White', 'size':'S','price':55
    }
>>> product_two = {
    'name':'Shoes', 'color':'Black/White', 'size':8.5,'price':120
    }
>>> collections.insert_many([product_one, product_two])
```

### Finding data

```python
>>> results = collections.find()
>>> for r in results:
        print(r['price'])

75
55
120
>>> for r in results:
        print(r['name'])

Tiro Track Pants
Hoodie
Shoes
```

To find a specific product

```python
>>> results = collection.find({'name':'Shoes'})
>>> for r in results:
        print(r['color'])

Black/White
```

### Delete and Update data

Same as *insert_one* and *insert_many*, you can delete and update singles and more that one document using **_delete_one_**/**_delete_many_** and **_update_one_**/**_update_many_**  methods.



```python
>>> collections.delete_one({'name':'Shoes'})
>>> collections.delete_many({'name':'Tiro Track Pants'})
```

To update a specific field using **$set**

```python
>>> collections.update_one({'name':'Hoodie'}, {'$set': {'name':'Sweater'}})
```
<br>
- 1st argument -> field to search and replace
- 2nd argument -> new data