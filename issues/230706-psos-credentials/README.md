# PSOS Credentials Bug Or Change In Behavior In FMS 19.5



## Description

Until 19.4 a PSOS call opened multiple database files on the server with the exact same credentials as they were opened on the client. Since version 19.5 this is only the case for the database that initiates the call. All other files referenced in the script are opened as if there were initially closed. 

There is an [article in the community](https://community.claris.com/en/s/question/0D53w00005rIXYaCAO/psos-credentials-bug-or-change-in-behavior-in-fms-1952), along a few others regarding similar observations or problems.



## How to reproduce:

Upload the demo files to a FileMaker Server and open FileA from the client. Login with user 'AdminA' (case is not important), the password for all accounts used in this demo is simply 'x'. When the file opens, you login to FileB with 'AdminB' / 'x'.

Now run the "collect data" script and the result will be displayed in the json result field. If the data is noch matching the expected result, an error message will be displayed. New configurations will be added to the list on the left, existing ones will be updated. 

You can add a pause the script on the server so you have enough time to check the accounts in the Server Admin Console. 

<img src="./assets/FileA.png" alt="FileA" style="zoom:40%;" />

## About the Test

The test script first collects the account name and privileges locally from both files and then repeats this on the server by performing the collectData script on the server (psos). All results are aggregated into a json object which is then saved to the result field and is displayed after the script finishes. If the configuration (server platform and version) already exists, the result is updated or added to the list otherwise. 



## Another Issue

In older versions the account name of FileB is not correctly returned. Instead the account name of the database that is doing the psos call is returned and also displayed in the Server Admin Console.



## Contribution

If you have a configuration that is not listed here or any new finding related to this issue, please leave a comment in this discussion: https://github.com/fmgarage/fm-issues/discussions/6



## Results

| Configuration         | same account on server | return correct account name |
| --------------------- | ---------------------- | --------------------------- |
| Server 18.0.4 Windows | ✅                      | ❌                           |
| Server 19.4.2 Ubuntu  | ✅                      | ❌                           |
| Server 19.5.3 Windows | ❌                      | ✅                           |
| Server 20.1.1 Ubuntu  | ❌                      | ✅                           |
| Server 20.1.1 Windows | ❌                      | ✅                           |



