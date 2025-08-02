# utl-identify-changes-in-column-values-using-sas-and-sqlite
    %let pgm=utl-identify-changes-in-column-values-using-sas-and-sqlite;

    %stop_submission;

    Identify changes in column values using sas and sqlite

    SOLUTIONS

       1 r sqldf
       2 sas datastep
       3 other sql dialects


    https://tinyurl.com/3hfd24pt
    https://github.com/rogerjdeangelis/utl-identify-changes-in-column-values-using-sas-and-sqlite

    communities.sas
    https://tinyurl.com/5n8v2h99
    https://communities.sas.com/t5/SAS-Programming/Count-changes-in-column/m-p/748640#M235127

    /**************************************************************************************************************************/
    /* INPUT                      | PROCESS                                        | OUTPUT                                   */
    /* =====                      | =======                                        | ======                                   */
    /* SD1.HAVE                   | 1 R SQLF                                       | > want                                   */
    /* ID VALUE                   | ========                                       |   ID VALUE change                        */
    /*                            |                                                | 1  1    10      0                        */
    /*  1   10                    | proc datasets lib=sd1                          | 2  1    10      0                        */
    /*  1   10                    |  nolist nodetails;                             | 3  1    12      1                        */
    /*  1   12                    |  delete want;                                  | 4  1    12      0                        */
    /*  1   12                    | run;quit;                                      | 5  1    15      1                        */
    /*  1   15                    |                                                |                                          */
    /*                            | %utl_rbeginx;                                  |                                          */
    /* options                    | parmcards4;                                    | SAS                                      */
    /*  validvarname=upcase;      | library(haven)                                 | ID  VALUE CHANGE                         */
    /* libname sd1 "d:/sd1";      | library(sqldf)                                 |                                          */
    /* data sd1.have;             | source("c:/oto/fn_tosas9x.r")                  |  1    10     0                           */
    /*  input id value;           | options(sqldf.dll = "d:/dll/sqlean.dll")       |  1    10     0                           */
    /* cards4;                    | have<-read_sas("d:/sd1/have.sas7bdat")         |  1    12     1                           */
    /* 1 10                       | print(have)                                    |  1    12     0                           */
    /* 1 10                       | want<-sqldf('                                  |  1    15     1                           */
    /* 1 12                       | select                                         |                                          */
    /* 1 12                       |  id,                                           |                                          */
    /* 1 15                       |  value,                                        |                                          */
    /* ;;;;                       |  case                                          |                                          */
    /* run;quit;                  |   when value <>lag(value,1,value)              |                                          */
    /*                            |      over (order by rowid)                     |                                          */
    /*                            |   then 1                                       |                                          */
    /*                            |   else 0                                       |                                          */
    /*                            |  end as change                                 |                                          */
    /*                            | from have;                                     |                                          */
    /*                            | ')                                             |                                          */
    /*                            | want                                           |                                          */
    /*                            | fn_tosas9x(                                    |                                          */
    /*                            |       inp    = want                            |                                          */
    /*                            |      ,outlib ="d:/sd1/"                        |                                          */
    /*                            |      ,outdsn ="want"                           |                                          */
    /*                            |      )                                         |                                          */
    /*                            | ;;;;                                           |                                          */
    /*                            | %utl_rendx;                                    |                                          */
    /*                            |                                                |                                          */
    /*                            | proc print data=sd1.want;                      |                                          */
    /*                            | run;quit;                                      |                                          */
    /*                            |                                                |                                          */
    /*                            |-------------------------------------------------------------------------------------------*/
    /*                            | 2 SAS DATASTEP                                 |                                          */
    /*                            | ==============                                 | SD1.HAVE                                 */
    /*                            |                                                |                                          */
    /*                            | data want;                                     | VALUE    CHANGE                          */
    /*                            |  set sd1.have;                                 |                                          */
    /*                            |  by id value notsorted;                        |   10        0                            */
    /*                            |  change = first.value;                         |   10        0                            */
    /*                            |  if first.id then change=0;                    |   12        1                            */
    /*                            |  run;                                          |   12        0                            */
    /*                            |                                                |   15        1                            */
    /*                            |  proc print data=want noobs;                   |                                          */
    /*                            | run;quit;                                      |                                          */
    /*                            |                                                |                                          */
    /*                            |-------------------------------------------------------------------------------------------*/
    /*                            | 3 OTHER SQL DIALECTS                           |                                          */
    /*                            | ====================                           |                                          */
    /*                            |                                                |                                          */
    /*                            | see below                                      |                                          */
    /*                            |                                                |                                          */
    /*                            |                                                |                                          */
    /*                            |                                                |                                          */
    /*                            |                                                |                                          */
    /**************************************************************************************************************************/

    /*____         _   _                           _      _ _       _           _
    |___ /    ___ | |_| |__   ___ _ __   ___  __ _| |  __| (_) __ _| | ___  ___| |_ ___
      |_ \   / _ \| __| `_ \ / _ \ `__| / __|/ _` | | / _` | |/ _` | |/ _ \/ __| __/ __|
     ___) | | (_) | |_| | | |  __/ |    \__ \ (_| | || (_| | | (_| | |  __/ (__| |_\__ \
    |____/   \___/ \__|_| |_|\___|_|    |___/\__, |_| \__,_|_|\__,_|_|\___|\___|\__|___/
                                                |_|
    */

    Same code for
       python
       matlab(octave)
       pspp(spss with shelling out to postgresql)
       excel
       perl
       any database with a CLI?
       Any database via ODBC
       powershell wrapped odbc or CLIs

     by way of r, python
       MS acess
       SQLite
       MySQL & MariaDB
       PostgreSQL
       Microsoft SQL Server
       Oracle
       Amazon Redshift
       Apache Hive
       Apache Impala
       MongoDB
       Redis
       Sybase
       Firebird
       IBM DB2
       Any database via ODBC


    Related repos

    https://tinyurl.com/4e6yaap8

    github
    https://tinyurl.com/4t54tcfc
    https://github.com/rogerjdeangelis/utl-utl-interface-sqlite3-with-any-language-that-supports-host-commands

    github
    https://tinyurl.com/yxvwzhz7
    https://github.com/rogerjdeangelis/utl-drop-down-to-perl-and-summarize-a-sql-table-using-sqlite-file-database

    github
    https://tinyurl.com/3em6k2z7
    https://github.com/rogerjdeangelis/utl-export-ms-access-table-from-mdb-database-to-sas-table-without-sas-access-using-powershell

    github
    https://tinyurl.com/5mpbc23d
    https://github.com/rogerjdeangelis/utl-creating-sqlite-and-postgresql-tables-from-sas-datasets-without-sas-access-and-a-blueprint

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
dentify changes in column values using sas and sqlite
