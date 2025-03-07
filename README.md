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

