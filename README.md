# 1999_Czech_financial_dataset_Teradata

Real world transactions in the years 1993 to 1998 from a Czech bank, modified for loading into Teradata.

Some modifications done to make the data look more up-to-date:

 1. 20 years were added to each date resulting in a date range from 2003 to 2018
 2. Amounts (in Czech Crowns) were divided by 10, now they look similar to current $ or € amounts.
 3. Czech descriptions are translated to English abbreviations, e.g. `VYBER KARTOU` = `credit card withdrawal`= `CCW` (see column comments for actual values).
 
Based on the [Financial Data Set](http://sorry.vse.cz/~berka/challenge/pkdd1999/data_berka.zip) from [PKDD'99 Discovery Challenge.](https://sorry.vse.cz/~berka/challenge/pkdd1999/berka.htm).
This data was prepared by [Petr Berka](https://sorry.vse.cz/~berka/challenge/) and Marta Sochorova.

All files contain tab-delimited data:

    (4500 objects in the file fin_account.tsv) - each record describes static characteristics of an account,
    (5369 objects in the file fin_client.tsv) - each record describes characteristics of a client,
    (5369 objects in the file fin_disp.tsv) - each record relates together a client with an account,
    (6471 objects in the file fin_order.tsv) - each record describes characteristics of a payment order,
    (1056320 objects in the file fin_trans.tsv) - each record describes one transaction on an account,
    (682 objects in the file fin_loan.tsv) - each record describes a loan granted for a given account,
    (892 objects in the file fin_card.tsv) - each record describes a credit card issued to an account,
    (77 objects in the file fin_district.tsv) - each record describes demographic characteristics of a district.


## Prerequisites

 1. `BTEQ` must be installed on your client.

 2. The load user needs the `CREATE TABLE` right in the target database.

### Installing using a Windows client

 1. Download [financial_db_Teradata.zip](https://github.com/dnoeth/1999_Czech_financial_dataset_Teradata/blob/master/financial_db_Teradata.zip) and extract the zip file to a folder, e.g. `C:\Samples\financial_db_Teradata`.

 2. Modify the file `fin_install.btq` to match your target system. Optionally modify the database name.
 
 3. Open a *cmd* (or *PowerShell*) window, change to the folder and run the file using BTEQ:

```
cd C:\Samples\C:\Samples\financial_db_Teradata
bteq < fin_install.btq > fin_install.log
```

### Installing using a Linux client

 1. Download [financial_db_Teradata.zip]((https://github.com/dnoeth/1999_Czech_financial_dataset_Teradata/blob/master/financial_db_Teradata.zip)) and extract the zip file to a folder, e.g. `~/Samples/financial_db_Teradata`.

 2. Modify the file `fin_install.btq` to match your target system. Optionally modify the database name.
 
 3. Open a *terminal* window, change to the folder and run the file using BTEQ:
 
```
cd ~/Samples/financial_db_Teradata
bteq < fin_install.btq > fin_install.log
```


#### Checking for successful installation

The script should finish in a few minutes.

If the install is running without errors you will see this message repeated 8 times: 
```
 *** WARNING: OUT OF DATA.
```

Otherwise check the `fin_install.log` for errors

### Reinstalling

Before re-running the install script the tables must be dropped in a specific order due to the FK constraints

```
   DROP TABLE fin_card;
   DROP TABLE fin_loan;
   DROP TABLE fin_order;
   DROP TABLE fin_trans;
   DROP TABLE fin_disp;
   DROP TABLE fin_client;
   DROP TABLE fin_account;
   DROP TABLE fin_district;
```
