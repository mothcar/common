## Mongo DB

~~~~
$ sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10
$ echo 'deb http://downloads-distro.mongodb.org/repo/ubuntu-upstart dist 10gen' | sudo tee /etc/apt/sources.list.d/mongodb.list
$ sudo apt-get update
$ sudo apt-get install -y mongodb-org

$ mkdir /data/db
$ mongod --dbpath /data/db

// when use cloud server
$ mongod --smallfiles

$ service mongod stop
~~~~

[mongoose](https://developer.mozilla.org/en-US/docs/Learn/Server-side/Express_Nodejs/mongoose)

## mongolab
https://mlab.com/

database name : meeteamdb

tutorial :: 
[link](https://zellwk.com/blog/crud-express-mongodb/)

## command on Terminal
```
> show dbs
> use DBNAME
> show collections
> db.name.insert()
> db.name.find()
> db.name.find({name : 'want a name'})
```

## mongodb Cloud
https://cloud.mongodb.com/v2/592d01f4d383ad69bc742de9#clusters?tooltip=nds.ipwhitelist&step=0
root
1x4 + ax4
