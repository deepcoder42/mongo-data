# Python project containing program for data manipulation in a Mongo database.
# Classification (U)

# Description:
  Used to take an external JSON document and insert into a Mongo database, delete a document from a Mongo database collection based on passed key(s) and value(s), or truncate a collection within a Mongo database.


###  This README file is broken down into the following sections:
  * Features
  * Prerequisites
    - FIPS Environment
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
    - git
    - python-pip
    - python-devel

  * Local class/library dependencies within the program structure.
    - python-lib
    - mongo-lib

  * FIPS Environment:  If operating in a FIPS 104-2 environment, this package will require at least a minimum of pymongo==3.8.0 or better.  It will also require a manual change to the auth.py module in the pymongo package.  See below for changes to auth.py.
    - Locate the auth.py file python installed packages on the system in the pymongo package directory.
    - Edit the file and locate the \_password_digest function.
    - In the \_password_digest function there is an line that should match: "md5hash = hashlib.md5()".  Change it to "md5hash = hashlib.md5(usedforsecurity=False)".
    - Lastly, it will require the configuration file entry auth_mech to be set to: SCRAM-SHA-1 or SCRAM-SHA-256.


# Installation:

Install the project using git.
  * From here on out, any reference to **{Python_Project}** or **PYTHON_PROJECT** replace with the baseline path of the python program.

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
Make the appropriate change to the environment.
  * Make the appropriate changes to connect to a Mongo database.
    - user = "USER"
    - japd = "PWORD"
    - host = "HOST_IP"
    - name = "HOSTNAME"

  * Change these entries only if required:
    - port = 27017
    - conf_file = None
    - auth = True
    - auth_db = "admin"
    - auth_mech = "SCRAM-SHA-1"
    - use_arg = True
    - use_uri = False

  * If connecting to a Mongo replica set:
    - repset = "REPLICA_SET_NAME"
    - repset_hosts = "HOST_1:PORT, HOST_2:PORT, ..."
    - db_auth = "AUTHENTICATION_DATABASE"

  * Notes for auth_mech configuration entry:
    - NOTE 1:  SCRAM-SHA-256 only works for Mongodb 4.0 and better.
    - NOTE 2:  FIPS 140-2 environment requires SCRAM-SHA-1 or SCRAM-SHA-256.
    - NOTE 3:  MONGODB-CR is not supported in Mongodb 4.0 and better.

  * If using SSL connections then set one or more of the following entries.  This will automatically enable SSL connections. Below are the configuration settings for SSL connections.  See configuration file for details on each entry:
    - ssl_client_ca = None
    - ssl_client_key = None
    - ssl_client_cert = None
    - ssl_client_phrase = None

  * FIPS Environment for Mongo:  If operating in a FIPS 104-2 environment, this package will require at least a minimum of pymongo==3.8.0 or better.  It will also require a manual change to the auth.py module in the pymongo package.  See below for changes to auth.py.
    - Locate the auth.py file python installed packages on the system in the pymongo package directory.
    - Edit the file and locate the "_password_digest" function.
    - In the "\_password_digest" function there is an line that should match: "md5hash = hashlib.md5()".  Change it to "md5hash = hashlib.md5(usedforsecurity=False)".
    - Lastly, it will require the Mongo configuration file entry auth_mech to be set to: SCRAM-SHA-1 or SCRAM-SHA-256.

```
cd config
cp mongo.py.TEMPLATE mongo.py
vim mongo.py
chmod 600 mongo.py
```


# Program Help Function:

  The program has a -h (Help option) that will show display an usage message.  The help message will usually consist of a description, usage, arugments to the program, example, notes about the program, and any known bugs not yet fixed.  To run the help command:

```
{Python_Project}/mongo-data/mongo_db_data.py -h
```


# Testing:

# Unit Testing:

### Installation:

Install the project using the procedures in the Installation section.

### Testing:

```
cd {Python_Project}/mongo-data
test/unit/mongo_db_data/unit_test_run.sh
```

### Code coverage:

```
cd {Python_Project}/mongo-data
test/unit/mongo_db_data/code_coverage.sh
```
