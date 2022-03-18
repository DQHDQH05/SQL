<center>
    <img src="https://s3-api.us-geo.objectstorage.softlayer.net/cf-courses-data/CognitiveClass/Logos/organization_logo/organization_logo.png" width="300" alt="cognitiveclass.ai logo"  />
</center>

<h1 align=center><font size = 5>Assignment: Notebook for Peer Assignment</font></h1>


# Introduction

Using this Python notebook you will:

1.  Understand three Chicago datasets
2.  Load the three datasets into three tables in a Db2 database
3.  Execute SQL queries to answer assignment questions


## Understand the datasets

To complete the assignment problems in this notebook you will be using three datasets that are available on the city of Chicago's Data Portal:

1.  <a href="https://data.cityofchicago.org/Health-Human-Services/Census-Data-Selected-socioeconomic-indicators-in-C/kn9c-c2s2?utm_medium=Exinfluencer&utm_source=Exinfluencer&utm_content=000026UJ&utm_term=10006555&utm_id=NA-SkillsNetwork-Channel-SkillsNetworkCoursesIBMDeveloperSkillsNetworkDB0201ENSkillsNetwork20127838-2021-01-01">Socioeconomic Indicators in Chicago</a>
2.  <a href="https://data.cityofchicago.org/Education/Chicago-Public-Schools-Progress-Report-Cards-2011-/9xs2-f89t?utm_medium=Exinfluencer&utm_source=Exinfluencer&utm_content=000026UJ&utm_term=10006555&utm_id=NA-SkillsNetwork-Channel-SkillsNetworkCoursesIBMDeveloperSkillsNetworkDB0201ENSkillsNetwork20127838-2021-01-01">Chicago Public Schools</a>
3.  <a href="https://data.cityofchicago.org/Public-Safety/Crimes-2001-to-present/ijzp-q8t2?utm_medium=Exinfluencer&utm_source=Exinfluencer&utm_content=000026UJ&utm_term=10006555&utm_id=NA-SkillsNetwork-Channel-SkillsNetworkCoursesIBMDeveloperSkillsNetworkDB0201ENSkillsNetwork20127838-2021-01-01">Chicago Crime Data</a>

### 1. Socioeconomic Indicators in Chicago

This dataset contains a selection of six socioeconomic indicators of public health significance and a “hardship index,” for each Chicago community area, for the years 2008 – 2012.

A detailed description of this dataset and the original dataset can be obtained from the Chicago Data Portal at:
[https://data.cityofchicago.org/Health-Human-Services/Census-Data-Selected-socioeconomic-indicators-in-C/kn9c-c2s2](https://data.cityofchicago.org/Health-Human-Services/Census-Data-Selected-socioeconomic-indicators-in-C/kn9c-c2s2?utm_medium=Exinfluencer&utm_source=Exinfluencer&utm_content=000026UJ&utm_term=10006555&utm_id=NA-SkillsNetwork-Channel-SkillsNetworkCoursesIBMDeveloperSkillsNetworkDB0201ENSkillsNetwork20127838-2021-01-01&cm_mmc=Email_Newsletter-\_-Developer_Ed%2BTech-\_-WW_WW-\_-SkillsNetwork-Courses-IBMDeveloperSkillsNetwork-DB0201EN-SkillsNetwork-20127838&cm_mmca1=000026UJ&cm_mmca2=10006555&cm_mmca3=M12345678&cvosrc=email.Newsletter.M12345678&cvo_campaign=000026UJ)

### 2. Chicago Public Schools

This dataset shows all school level performance data used to create CPS School Report Cards for the 2011-2012 school year. This dataset is provided by the city of Chicago's Data Portal.

A detailed description of this dataset and the original dataset can be obtained from the Chicago Data Portal at:
[https://data.cityofchicago.org/Education/Chicago-Public-Schools-Progress-Report-Cards-2011-/9xs2-f89t](https://data.cityofchicago.org/Education/Chicago-Public-Schools-Progress-Report-Cards-2011-/9xs2-f89t?utm_medium=Exinfluencer&utm_source=Exinfluencer&utm_content=000026UJ&utm_term=10006555&utm_id=NA-SkillsNetwork-Channel-SkillsNetworkCoursesIBMDeveloperSkillsNetworkDB0201ENSkillsNetwork20127838-2021-01-01&cm_mmc=Email_Newsletter-\_-Developer_Ed%2BTech-\_-WW_WW-\_-SkillsNetwork-Courses-IBMDeveloperSkillsNetwork-DB0201EN-SkillsNetwork-20127838&cm_mmca1=000026UJ&cm_mmca2=10006555&cm_mmca3=M12345678&cvosrc=email.Newsletter.M12345678&cvo_campaign=000026UJ)

### 3. Chicago Crime Data

This dataset reflects reported incidents of crime (with the exception of murders where data exists for each victim) that occurred in the City of Chicago from 2001 to present, minus the most recent seven days.

A detailed description of this dataset and the original dataset can be obtained from the Chicago Data Portal at:
[https://data.cityofchicago.org/Public-Safety/Crimes-2001-to-present/ijzp-q8t2](https://data.cityofchicago.org/Public-Safety/Crimes-2001-to-present/ijzp-q8t2?utm_medium=Exinfluencer&utm_source=Exinfluencer&utm_content=000026UJ&utm_term=10006555&utm_id=NA-SkillsNetwork-Channel-SkillsNetworkCoursesIBMDeveloperSkillsNetworkDB0201ENSkillsNetwork20127838-2021-01-01&cm_mmc=Email_Newsletter-\_-Developer_Ed%2BTech-\_-WW_WW-\_-SkillsNetwork-Courses-IBMDeveloperSkillsNetwork-DB0201EN-SkillsNetwork-20127838&cm_mmca1=000026UJ&cm_mmca2=10006555&cm_mmca3=M12345678&cvosrc=email.Newsletter.M12345678&cvo_campaign=000026UJ)


### Download the datasets

This assignment requires you to have these three tables populated with a subset of the whole datasets.

In many cases the dataset to be analyzed is available as a .CSV (comma separated values) file, perhaps on the internet. Click on the links below to download and save the datasets (.CSV files):

*   <a href="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-DB0201EN-SkillsNetwork/labs/FinalModule_Coursera_V5/data/ChicagoCensusData.csv?utm_medium=Exinfluencer&utm_source=Exinfluencer&utm_content=000026UJ&utm_term=10006555&utm_id=NA-SkillsNetwork-Channel-SkillsNetworkCoursesIBMDeveloperSkillsNetworkDB0201ENSkillsNetwork20127838-2021-01-01" target="_blank">Chicago Census Data</a>

*   <a href="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-DB0201EN-SkillsNetwork/labs/FinalModule_Coursera_V5/data/ChicagoPublicSchools.csv?utm_medium=Exinfluencer&utm_source=Exinfluencer&utm_content=000026UJ&utm_term=10006555&utm_id=NA-SkillsNetwork-Channel-SkillsNetworkCoursesIBMDeveloperSkillsNetworkDB0201ENSkillsNetwork20127838-2021-01-01" target="_blank">Chicago Public Schools</a>

*   <a href="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-DB0201EN-SkillsNetwork/labs/FinalModule_Coursera_V5/data/ChicagoCrimeData.csv?utm_medium=Exinfluencer&utm_source=Exinfluencer&utm_content=000026UJ&utm_term=10006555&utm_id=NA-SkillsNetwork-Channel-SkillsNetworkCoursesIBMDeveloperSkillsNetworkDB0201ENSkillsNetwork20127838-2021-01-01" target="_blank">Chicago Crime Data</a>

**NOTE:** Ensure you have downloaded the datasets using the links above instead of directly from the Chicago Data Portal. The versions linked here are subsets of the original datasets and have some of the column names modified to be more database friendly which will make it easier to complete this assignment.


### Store the datasets in database tables

To analyze the data using SQL, it first needs to be stored in the database.

While it is easier to read the dataset into a Pandas dataframe and then PERSIST it into the database as we saw in Week 3 Lab 3, it results in mapping to default datatypes which may not be optimal for SQL querying. For example a long textual field may map to a CLOB instead of a VARCHAR.

Therefore, **it is highly recommended to manually load the table using the database console LOAD tool, as indicated in Week 2 Lab 1 Part II**. The only difference with that lab is that in Step 5 of the instructions you will need to click on create "(+) New Table" and specify the name of the table you want to create and then click "Next".

<img src = "https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-DB0201EN-SkillsNetwork/labs/FinalModule_Coursera_V5/images/LoadingData.png">

##### Now open the Db2 console, open the LOAD tool, Select / Drag the .CSV file for the first dataset, Next create a New Table, and then follow the steps on-screen instructions to load the data. Name the new tables as follows:

1.  **CENSUS_DATA**
2.  **CHICAGO_PUBLIC_SCHOOLS**
3.  **CHICAGO_CRIME_DATA**


### Connect to the database

Let us first load the SQL extension and establish a connection with the database

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
    [2K     [90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━[0m [32m1.6/1.6 MB[0m [31m51.1 MB/s[0m eta [36m0:00:00[0m
    [?25hCollecting importlib-metadata
      Downloading importlib_metadata-4.11.3-py3-none-any.whl (18 kB)
    Collecting greenlet!=0.4.17
      Downloading greenlet-1.1.2-cp37-cp37m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (150 kB)
    [2K     [90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━[0m [32m150.2/150.2 KB[0m [31m21.8 MB/s[0m eta [36m0:00:00[0m
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
%load_ext sql
```

In the next cell enter your db2 connection string. Recall you created Service Credentials for your Db2 instance in first lab in Week 3. From your Db2 service credentials copy everything after db2:// (except the double quote at the end) and paste it in the cell below after ibm_db_sa://

<img src ="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-DB0201EN-SkillsNetwork/labs/FinalModule_Coursera_V5/images/details.png">



```python
# Remember the connection string is of the format:
# %sql ibm_db_sa://my-username:my-password@my-hostname:my-port/my-db-name?security=SSL
# Enter the connection string for your Db2 on Cloud database instance below
%sql ibm_db_sa://lcx19626:juBLtvBQH7MULXxf@19af6446-6171-4641-8aba-9dcff8e1b6ff.c1ogj3sd0tgtu0lqde00.databases.appdomain.cloud:30699/bludb?security=SSL
```




    'Connected: lcx19626@bludb'



## Problems

Now write and execute SQL queries to solve assignment problems

### Problem 1

##### Find the total number of crimes recorded in the CRIME table.



```python
%sql SELECT count(*) FROM CRIME;
```

     * ibm_db_sa://lcx19626:***@19af6446-6171-4641-8aba-9dcff8e1b6ff.c1ogj3sd0tgtu0lqde00.databases.appdomain.cloud:30699/bludb
    Done.





<table>
    <thead>
        <tr>
            <th>1</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>533</td>
        </tr>
    </tbody>
</table>



### Problem 2

##### List community areas with per capita income less than 11000.



```python
%sql SELECT Community_Area_Name FROM SOCIOECONOMIC WHERE PER_CAPITA_INCOME < 11000;
```

     * ibm_db_sa://lcx19626:***@19af6446-6171-4641-8aba-9dcff8e1b6ff.c1ogj3sd0tgtu0lqde00.databases.appdomain.cloud:30699/bludb
    Done.





<table>
    <thead>
        <tr>
            <th>community_area_name</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>West Garfield Park</td>
        </tr>
        <tr>
            <td>South Lawndale</td>
        </tr>
        <tr>
            <td>Fuller Park</td>
        </tr>
        <tr>
            <td>Riverdale</td>
        </tr>
    </tbody>
</table>



### Problem 3

##### List all case numbers for crimes  involving minors?(children are not considered minors for the purposes of crime analysis)



```python
%sql SELECT CASE_NUMBER, DESCRIPTION, PRIMARY_TYPE FROM CRIME WHERE lcase(description) like '%minor';
```

     * ibm_db_sa://lcx19626:***@19af6446-6171-4641-8aba-9dcff8e1b6ff.c1ogj3sd0tgtu0lqde00.databases.appdomain.cloud:30699/bludb
    Done.





<table>
    <thead>
        <tr>
            <th>case_number</th>
            <th>description</th>
            <th>primary_type</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>HL266884</td>
            <td>SELL/GIVE/DEL LIQUOR TO MINOR</td>
            <td>LIQUOR LAW VIOL</td>
        </tr>
        <tr>
            <td>HK238408</td>
            <td>ILLEGAL CONSUMPTION BY MINOR</td>
            <td>LIQUOR LAW VIOL</td>
        </tr>
    </tbody>
</table>



### Problem 4

##### List all kidnapping crimes involving a child?



```python
%sql SELECT CASE_NUMBER, DESCRIPTION, PRIMARY_TYPE FROM CRIME WHERE \
PRIMARY_TYPE = 'KIDNAPPING' AND DESCRIPTION LIKE 'CHILD%';
```

     * ibm_db_sa://lcx19626:***@19af6446-6171-4641-8aba-9dcff8e1b6ff.c1ogj3sd0tgtu0lqde00.databases.appdomain.cloud:30699/bludb
    Done.





<table>
    <thead>
        <tr>
            <th>case_number</th>
            <th>description</th>
            <th>primary_type</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>HN144152</td>
            <td>CHILD ABDUCTION/STRANGER</td>
            <td>KIDNAPPING</td>
        </tr>
    </tbody>
</table>



### Problem 5

##### What kinds of crimes were recorded at schools?



```python
%sql SELECT CASE_NUMBER, DESCRIPTION, PRIMARY_TYPE,LOCATION_DESCRIPTION FROM CRIME \
WHERE LOCATION_DESCRIPTION LIKE '%SCHOOL%';
```

     * ibm_db_sa://lcx19626:***@19af6446-6171-4641-8aba-9dcff8e1b6ff.c1ogj3sd0tgtu0lqde00.databases.appdomain.cloud:30699/bludb
    Done.





<table>
    <thead>
        <tr>
            <th>case_number</th>
            <th>description</th>
            <th>primary_type</th>
            <th>location_description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>HL353697</td>
            <td>SIMPLE</td>
            <td>BATTERY</td>
            <td>SCHOOL, PUBLIC, GROUNDS</td>
        </tr>
        <tr>
            <td>HL725506</td>
            <td>PRO EMP HANDS NO/MIN INJURY</td>
            <td>BATTERY</td>
            <td>SCHOOL, PUBLIC, BUILDING</td>
        </tr>
        <tr>
            <td>HP716225</td>
            <td>SIMPLE</td>
            <td>BATTERY</td>
            <td>SCHOOL, PUBLIC, BUILDING</td>
        </tr>
        <tr>
            <td>HH639427</td>
            <td>SIMPLE</td>
            <td>BATTERY</td>
            <td>SCHOOL, PUBLIC, BUILDING</td>
        </tr>
        <tr>
            <td>JA460432</td>
            <td>SIMPLE</td>
            <td>BATTERY</td>
            <td>SCHOOL, PUBLIC, GROUNDS</td>
        </tr>
        <tr>
            <td>HS200939</td>
            <td>TO VEHICLE</td>
            <td>CRIMINAL DAMAGE</td>
            <td>SCHOOL, PUBLIC, GROUNDS</td>
        </tr>
        <tr>
            <td>HK577020</td>
            <td>POSS: HEROIN(WHITE)</td>
            <td>NARCOTICS</td>
            <td>SCHOOL, PUBLIC, GROUNDS</td>
        </tr>
        <tr>
            <td>HS305355</td>
            <td>MANU/DEL:CANNABIS 10GM OR LESS</td>
            <td>NARCOTICS</td>
            <td>SCHOOL, PUBLIC, BUILDING</td>
        </tr>
        <tr>
            <td>HT315369</td>
            <td>PRO EMP HANDS NO/MIN INJURY</td>
            <td>ASSAULT</td>
            <td>SCHOOL, PUBLIC, GROUNDS</td>
        </tr>
        <tr>
            <td>HR585012</td>
            <td>TO LAND</td>
            <td>CRIMINAL TRESPA</td>
            <td>SCHOOL, PUBLIC, GROUNDS</td>
        </tr>
        <tr>
            <td>HH292682</td>
            <td>BOMB THREAT</td>
            <td>PUBLIC PEACE VI</td>
            <td>SCHOOL, PRIVATE, BUILDING</td>
        </tr>
        <tr>
            <td>G635735</td>
            <td>BOMB THREAT</td>
            <td>PUBLIC PEACE VI</td>
            <td>SCHOOL, PUBLIC, BUILDING</td>
        </tr>
    </tbody>
</table>



### Problem 6

##### List the average safety score for all types of schools.



```python
%sql select AVG(safety_score) as average_safety_score from SCHOOL
```

     * ibm_db_sa://lcx19626:***@19af6446-6171-4641-8aba-9dcff8e1b6ff.c1ogj3sd0tgtu0lqde00.databases.appdomain.cloud:30699/bludb
    Done.





<table>
    <thead>
        <tr>
            <th>average_safety_score</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>49</td>
        </tr>
    </tbody>
</table>



### Problem 7

##### List 5 community areas with highest % of households below poverty line



```python
%sql select COMMUNITY_AREA_NAME from SOCIOECONOMIC \
order by PERCENT_HOUSEHOLDS_BELOW_POVERTY DESC LIMIT 5;
```

     * ibm_db_sa://lcx19626:***@19af6446-6171-4641-8aba-9dcff8e1b6ff.c1ogj3sd0tgtu0lqde00.databases.appdomain.cloud:30699/bludb
    Done.





<table>
    <thead>
        <tr>
            <th>community_area_name</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Riverdale</td>
        </tr>
        <tr>
            <td>Fuller Park</td>
        </tr>
        <tr>
            <td>Englewood</td>
        </tr>
        <tr>
            <td>North Lawndale</td>
        </tr>
        <tr>
            <td>East Garfield Park</td>
        </tr>
    </tbody>
</table>



### Problem 8

##### Which community area is most crime prone?



```python
%sql select COMMUNITY_AREA_NUMBER, count(case_number) as no_of_cases from CRIME \
group by COMMUNITY_AREA_NUMBER order by no_of_cases desc limit 1
```

     * ibm_db_sa://lcx19626:***@19af6446-6171-4641-8aba-9dcff8e1b6ff.c1ogj3sd0tgtu0lqde00.databases.appdomain.cloud:30699/bludb
    Done.





<table>
    <thead>
        <tr>
            <th>community_area_number</th>
            <th>no_of_cases</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>25</td>
            <td>43</td>
        </tr>
    </tbody>
</table>



Double-click **here** for a hint

<!--
Query for the 'community area number' that is most crime prone.
-->


### Problem 9

##### Use a sub-query to find the name of the community area with highest hardship index



```python
%sql select COMMUNITY_AREA_NAME FROM SOCIOECONOMIC Where \
HARDSHIP_INDEX = (select MAX(HARDSHIP_INDEX) from SOCIOECONOMIC) 
```

     * ibm_db_sa://lcx19626:***@19af6446-6171-4641-8aba-9dcff8e1b6ff.c1ogj3sd0tgtu0lqde00.databases.appdomain.cloud:30699/bludb
    Done.





<table>
    <thead>
        <tr>
            <th>community_area_name</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Riverdale</td>
        </tr>
    </tbody>
</table>



### Problem 10

##### Use a sub-query to determine the Community Area Name with most number of crimes?



```python
%sql select S.COMMUNITY_AREA_NUMBER, S.COMMUNITY_AREA_NAME FROM SOCIOECONOMIC S\
where S.COMMUNITY_AREA_NUMBER = 25
```

     * ibm_db_sa://lcx19626:***@19af6446-6171-4641-8aba-9dcff8e1b6ff.c1ogj3sd0tgtu0lqde00.databases.appdomain.cloud:30699/bludb
    Done.





<table>
    <thead>
        <tr>
            <th>community_area_number</th>
            <th>community_area_name</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>25</td>
            <td>Austin</td>
        </tr>
    </tbody>
</table>



Copyright © 2020 [cognitiveclass.ai](cognitiveclass.ai?utm_source=bducopyrightlink&utm_medium=dswb&utm_campaign=bdu). This notebook and its source code are released under the terms of the [MIT License](https://bigdatauniversity.com/mit-license?utm_medium=Exinfluencer&utm_source=Exinfluencer&utm_content=000026UJ&utm_term=10006555&utm_id=NA-SkillsNetwork-Channel-SkillsNetworkCoursesIBMDeveloperSkillsNetworkDB0201ENSkillsNetwork20127838-2021-01-01&cm_mmc=Email_Newsletter-\_-Developer_Ed%2BTech-\_-WW_WW-\_-SkillsNetwork-Courses-IBMDeveloperSkillsNetwork-DB0201EN-SkillsNetwork-20127838&cm_mmca1=000026UJ&cm_mmca2=10006555&cm_mmca3=M12345678&cvosrc=email.Newsletter.M12345678&cvo_campaign=000026UJ).


## Author(s)

<h4> Hima Vasudevan </h4>
<h4> Rav Ahuja </h4>
<h4> Ramesh Sannreddy </h4>

## Contribtuor(s)

<h4> Malika Singla </h4>

## Change log

| Date       | Version | Changed by        | Change Description                             |
| ---------- | ------- | ----------------- | ---------------------------------------------- |
| 2021-11-17 | 2.6     | Lakshmi           | Updated library                                |
| 2021-05-19 | 2.4     | Lakshmi Holla     | Updated the question                           |
| 2021-04-30 | 2.3     | Malika Singla     | Updated the libraries                          |
| 2021-01-15 | 2.2     | Rav Ahuja         | Removed problem 11 and fixed changelog         |
| 2020-11-25 | 2.1     | Ramesh Sannareddy | Updated the problem statements, and datasets   |
| 2020-09-05 | 2.0     | Malika Singla     | Moved lab to course repo in GitLab             |
| 2018-07-18 | 1.0     | Rav Ahuja         | Several updates including loading instructions |
| 2018-05-04 | 0.1     | Hima Vasudevan    | Created initial version                        |

## <h3 align="center"> © IBM Corporation 2020. All rights reserved. <h3/>

