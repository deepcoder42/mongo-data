# Python project containing program for data manipulation in a Mongo database.
# Classification (U)

# Description:
  This program is used to take an external JSON document and insert into a Mongo database, delete a document from a Mongo database collection based on passed key(s) and value(s), or truncate a collection within a Mongo database.


###  This README file is broken down into the following sections:
  * Features
  * Prerequisites
  * Installation
  * Configuration
  * Program Help Function
  * Testing
    - Unit


# Features:
  * Insert JSON document into database.
  * Truncate collection in database.
  * Delete JSON document from database.

# Prerequisites:

  * List of Linux packages that need to be installed on the server.
    - python-libs
    - python-devel
    - git
    - python-pip

  * Local class/library dependencies within the program structure.
    - lib/arg_parser
    - lib/gen_libs
    - lib/cmds_gen
    - mongo_lib/mongo_class
    - mongo_lib/mongo_libs


# Installation:

Install the project using git.
  * Replace **{Python_Project}** with the baseline path of the python program.

```
umask 022
cd {Python_Project}
git clone git@github.com:deepcoder42/mongo-data.git
```

Install/upgrade system modules.

```
cd mongo-data
sudo bash
umask 022
pip install -r requirements.txt --upgrade --system
exit
```

Install supporting classes and libraries.
```
pip install -r requirements-python-lib.txt --target lib --system
pip install -r requirements-mongo-lib.txt --target mongo_lib --system
pip install -r requirements-python-lib.txt --target mongo_lib/lib --system
```

# Configuration:

Create Mongodb configuration file.
```
cd config
cp mongo.py.TEMPLATE mongo.py
```

Make the appropriate change to the environment.
  * Make the appropriate changes to connect to a Mongo database.
    - user = "USER"
    - passwd = "PASSWORD"
    - host = "IP_ADDRESS"
    - name = "HOSTNAME"

  * If connecting to a Mongo replica set, otherwise set to None.
    - repset = "REPLICA_SET_NAME"
    - repset_hosts = "HOST_1:PORT, HOST_2:PORT, ..."
    - db_auth = "AUTHENTICATION_DATABASE"

```
vim mongo.py
chmod 600 mongo.py
```


# Program Help Function:

  The program has a -h (Help option) that will show display an usage message.  The help message will usually consist of a description, usage, arugments to the program, example, notes about the program, and any known bugs not yet fixed.  To run the help command:
  * Replace **{Python_Project}** with the baseline path of the python program.

```
{Python_Project}/mongo-data/mongo_db_data.py -h
```


# Testing:


# Unit Testing:

### Description: Testing consists of unit testing for the functions in the mongo_db_data.py program.

### Installation:

Install the project using git.
  * Replace **{Python_Project}** with the baseline path of the python program.
  * Replace **{Branch_Name}** with the name of the Git branch being tested.  See Git Merge Request.

```
umask 022
cd {Python_Project}
git clone --branch {Branch_Name} git@github.com:deepcoder42/mongo-data.git
```

Install/upgrade system modules.

```
cd mongo-data
sudo bash
umask 022
pip install -r requirements.txt --upgrade --system
exit
```

Install supporting classes and libraries.

```
pip install -r requirements-python-lib.txt --target lib --system
pip install -r requirements-mongo-lib.txt --target mongo_lib --system
pip install -r requirements-python-lib.txt --target mongo_lib/lib --system
```


# Unit test runs for mongo_db_data.py:
  * Replace **{Python_Project}** with the baseline path of the python program.

```
cd {Python_Project}/mongo-data
test/unit/mongo_db_data/delete_docs.py
test/unit/mongo_db_data/get_repset_hosts.py
test/unit/mongo_db_data/get_repset_name.py
test/unit/mongo_db_data/help_message.py
test/unit/mongo_db_data/insert_doc.py
test/unit/mongo_db_data/main.py
test/unit/mongo_db_data/process_args.py
test/unit/mongo_db_data/run_program.py
test/unit/mongo_db_data/truncate_coll.py
```

### All unit testing
```
test/unit/mongo_db_data/unit_test_run.sh
```

### Code coverage program
```
test/unit/mongo_db_data/code_coverage.sh
```

