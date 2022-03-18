<center>
    <img src="https://s3-api.us-geo.objectstorage.softlayer.net/cf-courses-data/CognitiveClass/Logos/organization_logo/organization_logo.png" width="300" alt="cognitiveclass.ai logo"  />
</center>

# Connect to Db2 database on Cloud using Python

Estimated time needed: **15** minutes

## Objectives

After completing this lab you will be able to:

*   Import the ibm_db Python library
*   Enter the database connection credentials
*   Create the database connection
*   Close the database connection


**Note:** Please follow the instructions given in the first Lab of this course to Create a database service instance of Db2 on Cloud and retrieve your database Service Credentials.

## Import the `ibm_db` Python library

The `ibm_db` [API ](https://pypi.python.org/pypi/ibm_db/?utm_medium=Exinfluencer&utm_source=Exinfluencer&utm_content=000026UJ&utm_term=10006555&utm_id=NA-SkillsNetwork-Channel-SkillsNetworkCoursesIBMDeveloperSkillsNetworkDB0201ENSkillsNetwork20127838-2021-01-01) provides a variety of useful Python functions for accessing and manipulating data in an IBM® data server database, including functions for connecting to a database, preparing and issuing SQL statements, fetching rows from result sets, calling stored procedures, committing and rolling back transactions, handling errors, and retrieving metadata.

We first import the ibm_db library into our Python Application

Execute the following cells by clicking within it and then
press `Shift` and `Enter` keys simultaneously

The following required modules are pre-installed in the Skills Network Labs environment. However if you run this notebook commands in a different Jupyter environment (e.g. Watson Studio or Ananconda) you may need to install these libraries by removing the `#` sign before `!pip` in the code cell below.



```python
# These libraries are pre-installed in SN Labs. If running in another environment please uncomment lines below to install them:
!pip install --force-reinstall ibm_db==3.1.0 ibm_db_sa==0.3.3
# Ensure we don't load_ext with sqlalchemy>=1.4 (incompadible)
!pip uninstall sqlalchemy==1.4 -y && pip install sqlalchemy==1.3.24
!pip install ipython-sql
```

    Collecting ibm_db==3.1.0
      Using cached ibm_db-3.1.0-cp37-cp37m-linux_x86_64.whl
    Collecting ibm_db_sa==0.3.3
      Using cached ibm_db_sa-0.3.3-py3-none-any.whl
    Collecting sqlalchemy>=0.7.3
      Downloading SQLAlchemy-1.4.32-cp37-cp37m-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_17_x86_64.manylinux2014_x86_64.whl (1.6 MB)
    [2K     [90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━[0m [32m1.6/1.6 MB[0m [31m67.5 MB/s[0m eta [36m0:00:00[0m
    [?25hCollecting importlib-metadata
      Downloading importlib_metadata-4.11.3-py3-none-any.whl (18 kB)
    Collecting greenlet!=0.4.17
      Downloading greenlet-1.1.2-cp37-cp37m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (150 kB)
    [2K     [90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━[0m [32m150.2/150.2 KB[0m [31m28.3 MB/s[0m eta [36m0:00:00[0m
    [?25hCollecting typing-extensions>=3.6.4
      Downloading typing_extensions-4.1.1-py3-none-any.whl (26 kB)
    Collecting zipp>=0.5
      Downloading zipp-3.7.0-py3-none-any.whl (5.3 kB)
    Installing collected packages: ibm_db, zipp, typing-extensions, greenlet, importlib-metadata, sqlalchemy, ibm_db_sa
      Attempting uninstall: ibm_db
        Found existing installation: ibm-db 3.1.0
        Uninstalling ibm-db-3.1.0:
          Successfully uninstalled ibm-db-3.1.0
      Attempting uninstall: zipp
        Found existing installation: zipp 3.7.0
        Uninstalling zipp-3.7.0:
          Successfully uninstalled zipp-3.7.0
      Attempting uninstall: typing-extensions
        Found existing installation: typing_extensions 4.1.1
        Uninstalling typing_extensions-4.1.1:
          Successfully uninstalled typing_extensions-4.1.1
      Attempting uninstall: importlib-metadata
        Found existing installation: importlib-metadata 4.11.2
        Uninstalling importlib-metadata-4.11.2:
          Successfully uninstalled importlib-metadata-4.11.2
      Attempting uninstall: sqlalchemy
        Found existing installation: SQLAlchemy 1.3.24
        Uninstalling SQLAlchemy-1.3.24:
          Successfully uninstalled SQLAlchemy-1.3.24
      Attempting uninstall: ibm_db_sa
        Found existing installation: ibm-db-sa 0.3.3
        Uninstalling ibm-db-sa-0.3.3:
          Successfully uninstalled ibm-db-sa-0.3.3
    Successfully installed greenlet-1.1.2 ibm_db-3.1.0 ibm_db_sa-0.3.3 importlib-metadata-4.11.3 sqlalchemy-1.4.32 typing-extensions-4.1.1 zipp-3.7.0
    Found existing installation: SQLAlchemy 1.4.32
    Uninstalling SQLAlchemy-1.4.32:
      Successfully uninstalled SQLAlchemy-1.4.32
    Collecting sqlalchemy==1.3.24
      Using cached SQLAlchemy-1.3.24-cp37-cp37m-manylinux2010_x86_64.whl (1.3 MB)
    Installing collected packages: sqlalchemy
    Successfully installed sqlalchemy-1.3.24
    Requirement already satisfied: ipython-sql in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (0.3.9)
    Requirement already satisfied: ipython>=1.0 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from ipython-sql) (7.32.0)
    Requirement already satisfied: ipython-genutils>=0.1.0 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from ipython-sql) (0.2.0)
    Requirement already satisfied: prettytable in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from ipython-sql) (3.1.1)
    Requirement already satisfied: six in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from ipython-sql) (1.16.0)
    Requirement already satisfied: sqlalchemy>=0.6.7 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from ipython-sql) (1.3.24)
    Requirement already satisfied: sqlparse in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from ipython-sql) (0.4.2)
    Requirement already satisfied: jedi>=0.16 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from ipython>=1.0->ipython-sql) (0.18.1)
    Requirement already satisfied: prompt-toolkit!=3.0.0,!=3.0.1,<3.1.0,>=2.0.0 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from ipython>=1.0->ipython-sql) (3.0.27)
    Requirement already satisfied: pexpect>4.3 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from ipython>=1.0->ipython-sql) (4.8.0)
    Requirement already satisfied: pickleshare in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from ipython>=1.0->ipython-sql) (0.7.5)
    Requirement already satisfied: traitlets>=4.2 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from ipython>=1.0->ipython-sql) (5.1.1)
    Requirement already satisfied: backcall in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from ipython>=1.0->ipython-sql) (0.2.0)
    Requirement already satisfied: decorator in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from ipython>=1.0->ipython-sql) (5.1.1)
    Requirement already satisfied: pygments in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from ipython>=1.0->ipython-sql) (2.11.2)
    Requirement already satisfied: setuptools>=18.5 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from ipython>=1.0->ipython-sql) (60.9.3)
    Requirement already satisfied: matplotlib-inline in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from ipython>=1.0->ipython-sql) (0.1.3)
    Requirement already satisfied: wcwidth in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from prettytable->ipython-sql) (0.2.5)
    Requirement already satisfied: importlib-metadata in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from prettytable->ipython-sql) (4.11.3)
    Requirement already satisfied: parso<0.9.0,>=0.8.0 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from jedi>=0.16->ipython>=1.0->ipython-sql) (0.8.3)
    Requirement already satisfied: ptyprocess>=0.5 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from pexpect>4.3->ipython>=1.0->ipython-sql) (0.7.0)
    Requirement already satisfied: typing-extensions>=3.6.4 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from importlib-metadata->prettytable->ipython-sql) (4.1.1)
    Requirement already satisfied: zipp>=0.5 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from importlib-metadata->prettytable->ipython-sql) (3.7.0)



```python
import ibm_db
```

When the command above completes, the `ibm_db` library is loaded in your notebook.

## Identify the database connection credentials

Connecting to dashDB or DB2 database requires the following information:

*   Driver Name
*   Database name
*   Host DNS name or IP address
*   Host port
*   Connection protocol
*   User ID (or username)
*   User Password

**Notice:** To obtain credentials please refer to the instructions given in the first Lab of this course

Now enter your database credentials below and execute the cell with `Shift` + `Enter`



```python
#Replace the placeholder values with your actual Db2 hostname, username, and password:
dsn_hostname = "19af6446-6171-4641-8aba-9dcff8e1b6ff.c1ogj3sd0tgtu0lqde00.databases.appdomain.cloud" # e.g.: "54a2f15b-5c0f-46df-8954-7e38e612c2bd.c1ogj3sd0tgtu0lqde00.databases.appdomain.cloud"
dsn_uid = "lcx19626"        # e.g. "abc12345"
dsn_pwd = "juBLtvBQH7MULXxf"      # e.g. "7dBZ3wWt9XN6$o0J"

dsn_driver = "{IBM DB2 ODBC DRIVER}"
dsn_database = "bludb"            # e.g. "BLUDB"
dsn_port = "30699"                # e.g. "32733" 
dsn_protocol = "TCPIP"            # i.e. "TCPIP"
dsn_security = "SSL"              #i.e. "SSL"
```

## Create the DB2 database connection

Ibm_db API uses the IBM Data Server Driver for ODBC and CLI APIs to connect to IBM DB2 and Informix.

Lets build the dsn connection string using the credentials you entered above



```python
#DO NOT MODIFY THIS CELL. Just RUN it with Shift + Enter
#Create the dsn connection string
dsn = (
    "DRIVER={0};"
    "DATABASE={1};"
    "HOSTNAME={2};"
    "PORT={3};"
    "PROTOCOL={4};"
    "UID={5};"
    "PWD={6};"
    "SECURITY={7};").format(dsn_driver, dsn_database, dsn_hostname, dsn_port, dsn_protocol, dsn_uid, dsn_pwd,dsn_security)

#print the connection string to check correct values are specified
print(dsn)
```

    DRIVER={IBM DB2 ODBC DRIVER};DATABASE=bludb;HOSTNAME=19af6446-6171-4641-8aba-9dcff8e1b6ff.c1ogj3sd0tgtu0lqde00.databases.appdomain.cloud;PORT=30699;PROTOCOL=TCPIP;UID=lcx19626;PWD=juBLtvBQH7MULXxf;SECURITY=SSL;


Now establish the connection to the database



```python
#DO NOT MODIFY THIS CELL. Just RUN it with Shift + Enter
#Create database connection

try:
    conn = ibm_db.connect(dsn, "", "")
    print ("Connected to database: ", dsn_database, "as user: ", dsn_uid, "on host: ", dsn_hostname)

except:
    print ("Unable to connect: ", ibm_db.conn_errormsg() )

```

    Connected to database:  bludb as user:  lcx19626 on host:  19af6446-6171-4641-8aba-9dcff8e1b6ff.c1ogj3sd0tgtu0lqde00.databases.appdomain.cloud


Congratulations if you were able to connect successfuly. Otherwise check the error and try again.



```python
#Retrieve Metadata for the Database Server
server = ibm_db.server_info(conn)

print ("DBMS_NAME: ", server.DBMS_NAME)
print ("DBMS_VER:  ", server.DBMS_VER)
print ("DB_NAME:   ", server.DB_NAME)
```

    DBMS_NAME:  DB2/LINUXX8664
    DBMS_VER:   11.05.0600
    DB_NAME:    BLUDB



```python
#Retrieve Metadata for the Database Client / Driver
client = ibm_db.client_info(conn)

print ("DRIVER_NAME:          ", client.DRIVER_NAME) 
print ("DRIVER_VER:           ", client.DRIVER_VER)
print ("DATA_SOURCE_NAME:     ", client.DATA_SOURCE_NAME)
print ("DRIVER_ODBC_VER:      ", client.DRIVER_ODBC_VER)
print ("ODBC_VER:             ", client.ODBC_VER)
print ("ODBC_SQL_CONFORMANCE: ", client.ODBC_SQL_CONFORMANCE)
print ("APPL_CODEPAGE:        ", client.APPL_CODEPAGE)
print ("CONN_CODEPAGE:        ", client.CONN_CODEPAGE)
```

    DRIVER_NAME:           libdb2.a
    DRIVER_VER:            11.05.0500
    DATA_SOURCE_NAME:      BLUDB
    DRIVER_ODBC_VER:       03.51
    ODBC_VER:              03.01.0000
    ODBC_SQL_CONFORMANCE:  EXTENDED
    APPL_CODEPAGE:         1208
    CONN_CODEPAGE:         1208


## Close the Connection

We free all resources by closing the connection. Remember that it is always important to close connections so that we can avoid unused connections taking up resources.



```python
ibm_db.close(conn)
```




    True



## Summary

In this tutorial you established a connection to a DB2 database on Cloud database from a Python notebook using ibm_db API.


## Author

<a href="https://www.linkedin.com/in/ravahuja?utm_medium=Exinfluencer&utm_source=Exinfluencer&utm_content=000026UJ&utm_term=10006555&utm_id=NA-SkillsNetwork-Channel-SkillsNetworkCoursesIBMDeveloperSkillsNetworkDB0201ENSkillsNetwork20127838-2021-01-01">Rav Ahuja</a>

## Change Log

| Date (YYYY-MM-DD) | Version | Changed By | Change Description                 |
| ----------------- | ------- | ---------- | ---------------------------------- |
| 2021-11-17        | 2.2     | Lakshmi    | Updated library                    |
| 2021-07-09        | 2.1     | Malika     | Updated the connection string      |
| 2020-08-28        | 2.0     | Lavanya    | Moved lab to course repo in GitLab |

<hr>

## <h3 align="center"> © IBM Corporation 2020. All rights reserved. <h3/>

