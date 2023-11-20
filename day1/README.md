# BUILD LLM Bootcamp 2023

This repository contains instructions, code and data required to successfully complete BUILD LLM Bootcamp 2023.

## Day 1: Deploy Llama 2 from Hugging Face in Snowpark Container Services

### Prerequisites

* Laptop with wifi and ability to download libraries and Python packages from the web
* Docker Desktop (https://docs.docker.com/desktop/) installed
* VS Code (recommended) or other IDE
* A Hugging Face account (https://huggingface.co/)
Completed Llama 2 request form (https://ai.meta.com/resources/models-and-libraries/llama-downloads/). **NOTE**: Your Hugging Face account email address MUST match the email you provide on the Meta website or your request will not be approved
* After approval, submit the form (https://huggingface.co/meta-llama/Llama-2-7b-chat-hf) to access Llama 2 on Hugging Face to unlock access to the model. **NOTE**: This could take several hours.

### Snowpark Container Services (SPCS) User Account

Get exclusive access to Snowpark Container Services - currently in Private Preview - https://build-spcs.streamlit.app/ 

**NOTE**: If you are not able to get a SPCS user account, please still attend sessions on Day 1 and Day 2 and [earn the badge by completing the assessment](https://bit.ly/BUILD-LLM-Bootcamp2023).

### Hugging Face Token

Login into your account and access your Hugging Face token by browsing to Settings -> Access Tokens -> New token -- https://huggingface.co/settings/tokens

### Environment Setup

#### Step 1: Clone Repository

Clone this repository on your laptop and browse to the cloned folder.

#### Step 2: Create Conda Environment

In a terminal window, run the following command:

`conda create --name llm-bootcamp -c https://repo.anaconda.com/pkgs/snowflake python=3.9`

#### Step 3: Activate Conda Environment

In the same terminal window, run the following command:

`conda activate llm-bootcamp`

#### Step 4: Install Libraries

In the same terminal window, run the following command:

`conda install -c https://repo.anaconda.com/pkgs/snowflake snowflake-snowpark-python pandas notebook`

#### Step 5: Update Credentials

Update [connection.json](connection.json) with your Snowflake credentials based on the user account you have access to via "**Snowpark Container Services User Account**" section. Also update your Hugging Face token.

```json
{
  "account"   : "RTB37168",
  "user"      : "USER####",
  "password"  : "",
  "role"      : "ROLE_USER####",
  "warehouse" : "WH_XS_USER####",
  "database"  : "DB_USER####",
  "schema"    : "SCHEMA_LLM",
  "compute_pool" : "COMPUTE_POOL_USER####",
  "huggingface_token": ""
}
```

Replace `####` with your user number, set `password` and `huggingface_token`.

### Hands-on Lab: Deploy Llama 2 from Hugging Face in Snowpark Container Services

* Run `jupyter notebook` in the terminal window or open [llm-day1-notebook.ipynb](llm-day1-notebook.ipynb) in your favorite IDE.
* Select `llm-bootcamp` as your Notebook kernel
* Follow instructions and run through each cell in the Notebook

---

For questions and comments, please reach out to [Dash](dash.desai@snowflake.com).
