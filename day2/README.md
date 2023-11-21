## BUILD LLM Bootcamp 2023 Day 2: Fine-tune and Deploy Llama 2 in Snowpark Container Services

### Prerequisite

Successfully completed [BUILD LLM Bootcamp Day 1](https://github.com/Snowflake-Labs/build-llm-bootcamp-2023/blob/main/day1/README.md).

### Snowpark Container Services (SPCS) User Account

Get exclusive access to Snowpark Container Services - currently in Private Preview - by click on this link https://build-spcs.streamlit.app/.

**NOTE**: If you are not able to get a SPCS user account, you can still attend sessions on Day 1 and Day 2 to [earn the badge after completing the assessment](https://bit.ly/BUILD-LLM-Bootcamp2023) by December 8, 2023 11:59PM Pacific Time.

### Hands-on Lab

#### Step 1: Snowflake Login

Log into Snowflake account using your credentials -- [https://app.snowflake.com/sfsenorthamerica/build_spcs](https://app.snowflake.com/sfsenorthamerica/build_spcs)

#### Step 2: Create SQL Worksheet

After you log into your Snowflake account, click on **Worksheets** on the left navigation menu and then click on '+' button on top right and select **SQL Worksheet**.

#### Step 3: Select Database, Schema, and Warehouse

In the SQL Worksheet, run the following commands to select database, schema, and warehouse assigned to you:

```sql
use DB_USER####.SCHEMA_LLM;
use WAREHOUSE WH_XS_USER####;
```

NOTE: In the above SQL, replace `####` in database name and warehouse with your user number.

#### Step 4: Compute Pool Status

Check the status of your compute pool by running the following command:

```sql
show compute pools;
```

NOTE: If the state of your compute pool is STARTING or RESIZING, wait a few mins until it's in IDLE or ACTIVE state before proceeding.

#### Step 4: Free up Resources

Drop service from Day 1 to free up resources for Day 2 by running the following commands:

```sql
show services;
```

Assuming you have successfully completed hands-on lab from Day 1, the above command will list service that was created when you deployed Llama 2 from Hugging Face in SPCS. If that's the case, run the following command to drop that service.

```sql
drop service SERVICE_ID_GOES_HERE;
```

NOTE: The service ID should like something like SERVICE_FD43C8AA84BD11EE8E7CE246F4FD5A27

#### Step 5: Create Jupyter Notebook Service

Run the following command to create the service that will host the Jupyter Notebook which will be accessible via a public endpoint.

```sql
create service FINETUNE_LLM_SERVICE
  MIN_INSTANCES = 1
  MAX_INSTANCES = 1
  COMPUTE_POOL = COMPUTE_POOL_USER####"
  SPEC = '@yaml_stage/llm-bootcamp.yaml';
```

NOTE: In the above SQL, replace `####` in compute pool name with your user number.

#### Step 6: Jupyter Notebook Service Status

Run the following command to check the status of FINETUNE_LLM_SERVICE service

```sql
select 
  v.value:containerName::varchar container_name
  ,v.value:status::varchar status  
  ,v.value:message::varchar message
from (select parse_json(system$get_service_status('FINETUNE_LLM_SERVICE'))) t, 
lateral flatten(input => t.$1) v;
```

**NOTE**: Make sure the Status is set to READY and Message is set to Running before proceeding.

#### Step 7: Jupyter Notebook Service Endpoint

Run the following command to access the endpoint where Jupyter Notebook is hosted in SPCS.

```sql
show endpoints in service FINETUNE_LLM_SERVICE;
```

In the **Results** section look for a column named `ingress_url` and copy the URL. It should look something similar to `bab5b3y-sfsenorthamerica-build-spcs.snowflakecomputing.app`

**NOTE**: Make sure the Status is set to READY and Message is set to Running before proceeding.

### Hands-on Lab: Fine-tune and Deploy Llama 2 in Snowpark Container Services

* Open a new browser window and paste the Jupyter Notebook service endpoint URL copied in step 7
* Login using your Snowflake credentials
* On the left hand side, double click on [llm-day2-notebook.ipynb](llm-day2-notebook.ipynb)
* Follow instructions and run through each cell in the Notebook

