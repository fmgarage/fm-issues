# PSOS Credentials Bug Or Change In Behavior In FMS 19.5



## Description

Until 19.4 a PSOS call opened multiple database files on the server with the exact same credentials as they were opened on the client. Since version 19.5 this is only the case for the database that initiates the call. All other files that referenced in the script are opened as if there were initially closed. 

Starting from FileMaker Server 19.5 

## How to reproduce: