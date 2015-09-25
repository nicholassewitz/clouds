Pushes information from Amazon Redshift to Salesforce using Windows Dataloader CLI A very easy way to do this would be to set up a Windows EC2 Instance

Setup Instruction Download Data Loader login to salesforce go to setup search for data loader Under Data Management->Data Loader Download the windows version

Install Data Loader run windows setup for the dataloader for convenience, install it to c:\dataloader

PostgreSql Jar file download: postgresql.jdbc4.jar from postgresql website copy jar file to c:\dataloader\java\bin

Artsy Setup: Unzip artsy.zip under c:\dataloader setup permission to full permission for the Put_Salesforce_Account_Name_Here folder for everyone

Process runs: (first cd into c:\dataloader\artsy\bin)

following command runs individual object integration process

-Account Upsert: .\process.bat ../conf accountMasterProcess

-Account update: .\process.bat ../conf accountUpdateProcess

-Location upsert: .\process.bat ../conf locationProcess

-Contact upsert: .\process.bat ../conf contactProcess

-Fair upsert: .\process.bat ../conf fairProcess

-Show upsert: .\process.bat ../conf fairProcess

I created a daily batch file: redshift_daily_batch.bat, you can set this file to a windows scheduler call so it will run daily.

output is under c:\dataloader\Put_Salesforce_Account_Name_Here\status

Documentation process-conf.xml this file contains all our current salesforce integration objects. to add new ones, please change this file.

for production migration, sfdc.endpoint, sfdc.username, sfdc.password will need to be changed. to generated an encrypted password, please run c:\dataloader\Put_Salesforce_Account_Name_Here\bin\encrypt -e sfpwd and then copy the string into the password field.

database-conf.xml

this file contains all the redshift sql statements to collect data from redshift.

columns can be added to the sql or filter criteria can be added to the sql as well

xxxMap.sdl

this file is the redshift column to salesforce column mapper

every object will need a separate mapping file
