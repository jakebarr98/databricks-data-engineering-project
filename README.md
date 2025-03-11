# Databricks Earthquake Data Project

## Architecture

## Technology Used

## Dataset Used

## Step 1. Created Databricks resource
pricing tier = to enable connection to storage account, so we can leveridge role based access control (IAM) from storage account in data bricks

## Step 2. Created Storage Account resource & Storage Containers

bronze, silver and gold (Medallion architecture)

## Step 3. In storage account created new RBAC for databricks as storage blob contributor

## Step 4. In databricks, under catalogue > external data created new credentials

Credentials Type: Azure Managed Identity
Access connector ID: Databricks managed resourse group - unity-catalog-access-connector Resource ID

We can use this credential through the connector, we want to access an external location (storage containers in storage account)

created external locations, connecting to the bronze, silver and gold storage containers in storage account

use new storage credentials created in order to access them

## Step 5. Create compute resource

single node
single user

install package to libary in compute

## Step 6. Writing python notebooks
My next step was to write the scripts that would extract and transform my data. I wrote 3 notebooks, one for each of the containers.

### Bronze Notebook
![Bronze Python notebook](https://github.com/jakebarr98/databricks-data-engineering-project/blob/main/bronze%20notebook.ipynb)

In the bronze notebook I achieved the following:
Mounted datasets
Created variables for start and end date
Get data from API

I then saved the data to the Bronze container

### Silver Notebook
![Silver Python notebook](https://github.com/jakebarr98/databricks-data-engineering-project/blob/main/silver%20notebook.ipynb)

In the Silver notebook, I aimed to make small transformations to the data, making it more readable and easier to interact with as a developer. The transformations I achieved were as follows:
Changed column headings
Changed data types
Reshaped data in dataframe
Validated data - checked for null or missing values and assigned them value of 0

I then saved the data to the Silver container

### Gold Notebook
![Gold Python notebook](https://github.com/jakebarr98/databricks-data-engineering-project/blob/main/gold%20notebook.ipynb)
In the Gold notebook, I aimed to make more transformations, the purpose of which is to make the data more useful to the end user/business.
The transformations I achieved were as follows:

Retrieved country code via longiture & lattitude fields, using package installed on compute earlier (reverse_geocoder)
Categorised sig into a class using a conditional statement

This data was then saved to the Gold container

## Step 7. Create workflow

![Workflow Diagram]()

The next step was to create a workflow for my workbooks (tasks) to run one after another.

I went into the workflows section of databricks and created a new one, I added the activity of a notebook and assigned it to my compute, and to the Bronze notebook.

On success of the Bronze notebook running, I added another activity to run the Silver notebook

For this task, I had to add in the parameter for bronze_output - this is the path to the data in the Bronze storage container in the datalake I'd need to access to use in my silver transformations. I added the parameter below:
```ruby
bronze_output = {{tasks.Bronze_task.values.bronze_output}}
```

Folllowing the success of the Silver task, I created an activity for the Gold notebook to run, again, I had to add in variables to access the data in the Bronze and now Silver containers. 
```ruby
bronze_output = {{tasks.Bronze_task.values.bronze_output}}
silver_output = {{tasks.Silver_task.values.silver_output}}
```


