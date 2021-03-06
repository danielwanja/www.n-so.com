---
layout: post
title: "Amazon RDS: Amazon Relational Database Service or MySQL in the Cloud for Ruby On Rails."
date: 2009-10-29 03:02
comments: true
categories: cloud
---
For watchthatsite.com (not public yet) I have an instance on EC2 with Rails and MySQL but was looking for a more solid hosting solution for MySQL. And how fortunate, Amazon came out with the solution I need this week. Basically with two command line instructions you can start a new server with mysql configured, tuned, and secured. In this blog entry I will go through the steps that perform to move my sql database to Amazon RDS. 

<!--more-->

You can find more information on Amazon Relational Database Service (API Version 2009-10-16) <a href="http://developer.amazonwebservices.com/connect/entry.jspa?externalID=2927&categoryID=290">here</a>.

Prerequisite: you need to <a href="http://aws.amazon.com/">signup</a> for an account on aws.amazon.com, it can be used for EC2, S3, SimpleDb and all the other services AWS provides. 

<h2>1) Install the Command Line Toolkit</h2>

First thing, go download the command line toolkit and read the README.TXT on how to install it. In short you unzip the files, I did put mine at /Developer/aws/RDSCli-1.0.001. Then you create a credential file which contains your AWS access key id and secret key. Then I configured my ~/.bash_profile as follows:

```
export AWS_RDS_HOME=/Developer/aws/RDSCli-1.0.001
export AWS_CREDENTIAL_FILE=$AWS_RDS_HOME/credential-file-path.conf
export JAVA_HOME=/Library/Java/Home
export PATH=$AWS_RDS_HOME/bin:$PATH
```

to see that the command line toolkit is setup correctly type $rds --help

You will need the command line tool to execute several commands described here after.

 
<h2>2) Create an Instance</h2>

Let's create a MySQL Server instance. RDS offers the following 5 server instance classes:

* db.m1.small (1.7 GB of RAM, $0.11 per hour)
* db.m1.large (7.5 GB of RAM, $0.44 per hour)
* db.m1.xlarge (15 GB of RAM, $0.88 per hour)
* db.m2.2xlarge (34 GB of RAM, $1.55 per hour)
* db.m2.4xlarge (68 GB of RAM, $3.10 per hour)

I will choose a small instance which I will call dbserver1 with a database name db1 and allocate 5g of database space. I also set the master username as admin and password as secret.

```
$ rds-create-db-instance --db-instance-identifier db1 --allocated-storage 5 --db-instance-class db.m1.small --engine MySQL5.1 --master-username admin --master-user-password secret --db-name db1 --headers
```

The output is the following:

```
DBINSTANCE  DBInstanceId  Class        Engine    Storage  Master Username  Status    Backup Retention
DBINSTANCE  db1           db.m1.small  mysql5.1  5        admin            creating  1               
      SECGROUP  Name     Status
      SECGROUP  default  active
      PARAMGRP  Group Name        Apply Status
      PARAMGRP  default.mysql5.1  in-sync
```

Now you have a server running and you are being billed $0.11 per hour, that's like $80 a month without bandwidth but with backup...and it took only 2 minutes to get going. Can't beat that.

To see all the instances you have you can issue the 

```
rds-describe-db-instances --headers
```

<h2>3) Grant Network Access</h2>

So I will grant access from my notebook, assuming the ip address is 24.19.0.48 (you can also specify ranges i.e. 24.19.0.0/50). (Note that access was revoked by AWS, not sure why??)

```
rds-authorize-db-security-group-ingress default --cidr-ip 24.19.0.48 --headers
```

I also have an ec2 instance which I want to grant access to

```
rds-authorize-db-security-group-ingress default --ec2-security-group-name watchthatsite --ec2-security-group-owner-id 526541544691
```

Note the ec2-security-group-owner-id is your Amazon AWS account number, you can find it for example on you account activity page. To see your security configuration issue the following command: rds-describe-db-security-groups default --headers

<h2>4) Using the Database</h2>

To use your database you first need to find out the endpoint address of your new server. So describe you instances:  

```
rds-describe-db-instances --headers command
```

```
DBINSTANCE  DBInstanceId  Created                   Class        Engine    Storage  Master Username  Status     Endpoint Address                              Port  AZ          Backup Retention
DBINSTANCE  db1           2009-10-28T22:53:31.666Z  db.m1.small  mysql5.1  5        admin            available  db1.cyhik6zpub5c.us-east-1.rds.amazonaws.com  3306  us-east-1b  1               
      SECGROUP  Name     Status
      SECGROUP  default  active
      PARAMGRP  Group Name        Apply Status
      PARAMGRP  default.mysql5.1  in-sync
```

You find out your endpoint address, for me db1.cyhik6zpub5c.us-east-1.rds.amazonaws.com

So now you can connect to your database:

```
mysql -h db1.cyhik6zpub5c.us-east-1.rds.amazonaws.com -P 3306 -u admin -p db1
```

Let's configure my Rails application to point to that database and run a migration:

So I change my config/database.yml to point to the above database

```
development:
    adapter: mysql
    host: db1.cyhik6zpub5c.us-east-1.rds.amazonaws.com
    reconnect: false
    database: db1
    username: admin
    password: secret
```

```
 rake db:migrate
```
Wow, seem to work.


Let connect to the mysql console and do a show tables;

<pre>
+-------------------+
| Tables_in_db1     |
+-------------------+
| schema_migrations | 
| users             | 
| watches           | 
+-------------------+
</pre>

Yep, all there.

Now I still have to move my old production database to the new one, so let's dump the data from my old database:

```
mysqldump watchthatsite_development -u admin > wts.sql
```

and reload that data in the new database:

```
mysql -h db1.cyhik6zpub5c.us-east-1.rds.amazonaws.com -P 3306 -u admin -p db1 < wts.sql
```

Restarting my Rails serverâ€¦That's all!

Enjoy,
Daniel.


