# databricks-data-engineering-project
1. created databricks
pricing tier = to enable connection to storage account, so we can leveridge role based access control (IAM) from storage account in data bricks

2. created storage account & storage containers bronze, silver and gold (Medallion architecture)

3. In storage account created new RBAC for databricks as storage blob contributor

4. In databricks, under catalogue > external data created new credentials
  Credentials Type: Azure Managed Identity
  Access connector ID: Databricks managed resourse group - unity-catalog-access-connector Resource ID

We can use this credential through the connector, we want to access an external location (storage containers in storage account)

created external locations, connecting to the bronze, silver and gold storage containers in storage account

use new storage credentials created in order to access them

5. Create compute resource

single node
single user

install package to libary in compute

6. Write python scripts to transform data
notebook 1 - bronze
mount datasets
create variables for start and end date
get data from API

notebook 2 - silver
make small transformations to make data more readable
change column headings
change data types
reshaping data in dataframe
validating data - check for null or missing values and assign them value of 0
save data to silver container

notebook 3
make more transformations

retrieving country code using coordinates using package installed
categorising sig into class

8. create workflow
created workflow for workbooks to run one after another
bronze notebook runs, on success, silver notebook runs using parameter:

on success, gold notebook runs using parameters




