# Generative AI - Issue & Observability 

## Contents Overview

### Organization
1. I review the file contents of this project.
2. Data, raw and cleaned.
3. Installation of everything (assuming you have nothing).
4. Security! 
5. Vector DB setup (weaviate & nomic atlas)
6. Generative AI Account (cohere.ai)
7. Sqlite setup
8. Let's a go! (start running some scripts)

### Jupyter Notebooks
The notebook files are organized into dev and work directories.

I only used VSCode to develop this project.

### dev notebooks
All of the dev notebook files end with _dev.ipynb
These are files I wrote while developing this project. 
You may them useful 

### work notebooks
These are the working notebooks that contain the all necessary code
 to get you from A-Z.

These are also the files from which the article code snippets were taken.


## Data
Please see the LICENSE file (Apache 2.0)

You need clean data when you send it to the gen ai API or import into your vector database.
There are two data directories:
1. data\clean\
2. data\raw\

#### clean data
There are three files with cleaned data, suitable fo use during development
The number in the file name is the number of json objects (chat pairs) in each file.

1. data\clean\ShareGptChatPairs_2_clean_fmt.json
2. data\clean\ShareGptChatPairs_dev_10_cleaned.json
3. data\clean\ShareGptChatPairs_2415_cleaned.json

Cleaning data is covered in \dev\clean_data.ipynb



## Install Everything

### IDE
https://code.visualstudio.com/download 

Getting started with Jupyter in VSCOde
https://donjayamanne.github.io/pythonVSCodeDocs/docs/jupyter_getting-started/

Ctrl+Shit+P - Python
for handy python commands in vscode

#### Extensions
code --install-extension donjayamanne.python-environment-manager
code --install-extension donjayamanne.python-extension-pack
code --install-extension {YOUR_ACCT}Rose.vsc-python-indent
code --install-extension ms-python.python
code --install-extension ms-python.vscode-pylance
code --install-extension ms-toolsai.jupyter
code --install-extension ms-toolsai.jupyter-keymap
code --install-extension ms-toolsai.jupyter-renderers
code --install-extension ms-toolsai.vscode-jupyter-cell-tags
code --install-extension ms-toolsai.vscode-jupyter-slideshow

### Python
https://docs.conda.io/en/latest/miniconda.html 

#### Setting up a Development Environment for Python programming
https://www.pythonguis.com/tutorials/getting-started-vs-code-python/#:~:text=To%20use%20a%20virtual%20environment,selecting%20%3E%20Python%3A%20Select%20Interpreter%20.


#### Activate the python env in terminal (cmd|ps)
```PS
C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe -ExecutionPolicy ByPass -NoExit -Command "& 'C:\Users\{YOUR_ACCT}\miniconda3\shell\condabin\conda-hook.ps1' ; conda activate 'C:\Users\{YOUR_ACCT}\miniconda3' "
```
```cmd
C:\Windows\System32\cmd.exe "/K" C:\Users\{YOUR_ACCT}\miniconda3\Scripts\activate.bat C:\Users\{YOUR_ACCT}\miniconda3
```

#### Install Project's Python Requirements
Will install the correct versions of packages imported by this project

```bash
pip install -r requirements.txt
```


# Security!
API keys are stored in the .env file.
Note that the entries in the .env file do not use whitespace or quotes:
```
NOMIC_API_KEY=xjTl..{shhh it's a secret}................x_
```

Note that the .gitignore file contins this entry:
```
# api keys
.env
```

rename your_env to .env
add your api keys

Note this usage in 
```python
import os
from dotenv import load_dotenv
load_dotenv()
api_key = os.getenv('NOMIC_API_KEY')
```

Get your api keys from the URLs below


# Vector Database
Weaviate is a very easy-to-work-with vector db. I tried several of the usual suspects...

The feature I like the most is the ability to create a schema with any properties or fields that are needed, and choose which fields will be vectorized.

Weaviate was also super easy to use via docker. They also offer a cloud version.
make sure you have docker engine and docker-compose installed and in your PATH.
https://www.docker.com/products/docker-desktop/ 

Weaviate has a docker-compose configuration tool on their site: 
https://weaviate.io/developers/weaviate/installation/docker-compose

I have included my docker-compose.yml 

Then, from a cmd/ps/bash prompt:
```
docker-compose up -d
```



## Vector DB Visual Exploration
https://atlas.nomic.ai/

Click button labeled: Get Started with Atlas


## How to visualize weaviate data:
https://docs.nomic.ai/vector_database.html#weaviate

implemented here: 
 1. nomic.ipynb
 1. drift_nomic.ipynb




# Generative AI Account
I used an account on cohere.ai
Open https://cohere.com/ 
Click on Try Now button upper right corner

## The Cohere Platform
https://docs.cohere.com/docs

There's a simple script to verify that your setup can reach the API:

cohere_dev.ipynb




# SQLite
SQLite is used to store the time-series data generated when we run the benchmark sample every day or week or...

Setup incredibly simple:
https://www.sqlite.org/index.html

### Create a project db
A SQLite3 DB (\data\driftDb.db) is included. However, if you want to create your own: 
https://www.sqlite.org/quickstart.html



# Let's a go!
## DEV NOTEBOOKS


### Cleaning data with spaCy
https://spacy.io/ 
https://spacy.io/api/top-level 

Start by trying out the scripts in dev_nb\spacy_sentence_to_tokens_dev.ipynb.
This will show you how spaCy works. 

N.B. Note the use of spacy.prefer_gpu()
Will it make a difference in processing time?

Then run the scripts in dev_nb\spacy_sentence_to_tokens_dev.ipynb
This will show you the spacy functions I have used to clean the chat prompts and completions data in the \data\raw directory.

Once you're ready, you can get to work and clean and format the data!
work_nb\clean_data.ipynb



### NOMIC ATLAS
Atlas integrates with your workflow by organizing text, embedding datasets and creating interactive maps that can be explored in a web browser.

1. Make sure you get your login key
1. Make sure you have added the nomic login key to the .env file
1. Then run the code in dev_nb\nomic_start_here_dev.ipynb


### COHERE API
1. Make sure you get your login key
1. Make sure you have added the nomic login key to the .env file
1. Then run the code in dev_nb\cohere_dev.ipynb


### SQLITE
A few quick examples of sqlite: 
dev_nb\sqlite_db_dev.ipynb

Cleanup: 
dev_nb\sqlite_drop_all_tables.ipynb