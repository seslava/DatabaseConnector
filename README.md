DatabaseConnector
=================

[![CRAN_Status_Badge](http://www.r-pkg.org/badges/version/DatabaseConnector)](https://cran.r-project.org/package=DatabaseConnector)
[![CRAN_Status_Badge](http://cranlogs.r-pkg.org/badges/DatabaseConnector)](https://cran.r-project.org/package=DatabaseConnector)

Introduction
============
This R package provides function for connecting to various DBMSs. 

Features
========
- Create connections to the various database platforms:
  - MicrosoftSQL Server
  - Oracle
  - PostgresSql
  - Microsoft Parallel Data Warehouse (a.k.a. Analytics Platform System)
  - Amazon Redshift
  - Apache Impala(with Kerberos support)
  - Google BigQuery
  - IBM Netezza
  - Hive(with Kerberos support)
- Statements for executing queries with 
  - Error reporting to file
  - Progress reporting
  - Multiple statements per query
- Support for fetching data to ffdf objects
- Insert data frame to a database table
- Supports the DBI interface
- Integrates with RStudio's Connections tab

Examples
========
```r
connectionDetails <- createConnectionDetails(dbms="mysql", 
                                             server="localhost",
                                             user="root",
                                             password="blah",
                                             schema="cdm_v4")
conn <- connect(connectionDetails)
querySql(conn,"SELECT COUNT(*) FROM person")
disconnect(conn)
```

```r
## regular data insert
insertTable(connection = connection, 
            tableName = "scratch.somedata", 
            data = data, 
            dropTableIfExists = TRUE, 
            createTable = TRUE, 
            tempTable = FALSE, 
            useMppBulkLoad = FALSE)
            
## bulk data insert with Redshift or PDW
insertTable(connection = connection, 
            tableName = "scratch.somedata", 
            data = data, 
            dropTableIfExists = TRUE, 
            createTable = TRUE, 
            tempTable = FALSE, 
            useMppBulkLoad = TRUE)
```

Technology
============
DatabaseConnector is an R package using Java's JDBC drivers. 

System Requirements
===================
Requires R. Also requires Java 1.6 or higher (Oracle Java is recommended. [Issues](https://github.com/OHDSI/DatabaseConnector/issues/8) have been reported when using GCJ.) 

Dependencies
============
Please note that this package requires Java to be installed. If you don't have Java already intalled on your computed (on most computers it already is installed), go to [java.com](http://java.com) to get the latest version.

To be able to use Windows authentication for SQL Server, you have to install the JDBC driver. Download the .exe from [Microsoft](http://www.microsoft.com/en-us/download/details.aspx?displaylang=en&id=11774) and run it, thereby extracting its contents to a folder. In the extracted folder you will find the file sqljdbc_4.0/enu/auth/x64/sqljdbc_auth.dll (64-bits) or sqljdbc_4.0/enu/auth/x86/sqljdbc_auth.dll (32-bits), which needs to be moved to location on the system path, for example to c:/windows/system32.

DatabaseConnector also depends on the OHDSI DatabaseConnectorJars and SqlRender packages.

For Redshift Bulk Mpp inserts, the cloudyR aws S3 pacakge is required.

Getting Started
===============
To install the latest development version, install from GitHub:

```r
install.packages("devtools")

install.packages("https://github.com/InfoClinika/DatabaseConnectorJars/releases/download/v1.1.0/DatabaseConnectorJars_1.1.0-source.tar.gz", repo=NULL, type="source")
devtools::install_github("Infoclinika/DatabaseConnector")
```

Or you can download latest release from [DatabaseConnectorJars repository](https://github.com/InfoClinika/DatabaseConnectorJars/releases) and install it from local file

```r
install.packages("devtools")
 
install.packages("/path/to/file/DatabaseConnectorJars_1.1.0-source.tar.gz", repo=NULL, type="source")
devtools::install_github("Infoclinika/DatabaseConnector")
```

Getting Involved
================
* Vignette: [Using DatabaseConnector](https://github.com/OHDSI/DatabaseConnector/raw/master/inst/doc/UsingDatabaseConnector.pdf)
* Package manual: [DatabaseConnector manual](https://raw.githubusercontent.com/OHDSI/DatabaseConnector/master/extras/DatabaseConnector.pdf) 
* Developer questions/comments/feedback: <a href="http://forums.ohdsi.org/c/developers">OHDSI Forum</a>
* We use the <a href="../../issues">GitHub issue tracker</a> for all bugs/issues/enhancements

License
=======
DatabaseConnector is licensed under Apache License 2.0. The JDBC drivers [fall under their own respective licenses](https://raw.githubusercontent.com/OHDSI/DatabaseConnector/master/inst/COPYRIGHTS).

Development
===========
DatabaseConnector is being developed in R Studio.

### Development status
[![Build Status](https://travis-ci.org/OHDSI/DatabaseConnector.svg?branch=master)](https://travis-ci.org/OHDSI/DatabaseConnector)
[![codecov.io](https://codecov.io/github/OHDSI/DatabaseConnector/coverage.svg?branch=master)](https://codecov.io/github/OHDSI/DatabaseConnector?branch=master)

Stable. The code is actively being used in several projects.


# Acknowledgements
- This project is supported in part through the National Science Foundation grant IIS 1251151.

