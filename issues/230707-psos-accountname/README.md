# PSOS Account Name in related Files



## Description

In older versions the account name of FileB is not correctly returned. Instead the account name of the database that is doing the psos call is returned and also displayed in the Server Admin Console. This seems to be fixed in 19.5.

## How to reproduce:

Use the demo files from [Issue 230707](https://github.com/fmgarage/fm-issues/tree/main/issues/230706-psos-credentials).