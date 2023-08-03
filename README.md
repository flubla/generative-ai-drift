# Generative AI - Issue & Observability 

## Contents Overview

After you set up Python and VSCODE (as needed), set up 
  1. Weaviate
  2. Cohere account
  3. Nomic Atlas account
  4. SQLite

Confirm external resources are working by running the scipits in: [data\confirm_external_resources.ipynb](data\confirm_external_resources.ipynb)


Once it's all working, there are two paths you can follow:
1. Learn and experiment by using the notebooks in the *dev_nb* directory
2. ***Get straight to work creating the drift benchmarks*** with the notebooks in the *work_nb* directory.

There are README files in the *dev_nb* and *work_nb* directories.  
  

### Organization
1. What's in the project?
2. Development data
3. Installation of everything (assuming you have nothing).
4. API Key Security(.env) 
5. Vector DB Setup (Weaviate & Nomic atlas visualization)
6. Cohere Generative AI Account Setup
7. SQLite Setup
  


## 1. What's in the project?

### Jupyter Notebooks
* All code is contained within *.ipynb script files.
* These notebooks are organized into dev and work directories.
* VSCode was used to develop this project. 
* VSCODE extensions are listed below.

### Notebooks in *dev_nb*
All of the dev notebook files end with _dev.ipynb  

These are files I wrote while developing this project. 
You may them useful for learning and experimentation. 

### Notebooks in *work_nb*
These are the working notebooks that contain the all necessary code to get you from zer0 to drift benchmarks. These are also the files from which the article code snippets were taken.


### Development Data in *data*
You'll need clean data when you send it to the gen ai API or import into your vector database. 
All data is located in *data* directorY



## 2. Development Data
Data is licensed under [Apache 2.0](LICENSE). The license file is located in the *data* directory.

Data has been provided in a raw form and cleaned and formatted, ready for to use:

1. [data\clean\](data\clean\)
2. [data\raw\](data\raw\)

There are three files with cleaned data, suitable for use during development. The number in the file name is the number of json objects (chat pairs) in each file.

1. [data\clean\ShareGptChatPairs_2_clean_fmt.json](data\clean\ShareGptChatPairs_2_clean_fmt.json)
2. [data\clean\ShareGptChatPairs_dev_10_cleaned.json](data\clean\ShareGptChatPairs_dev_10_cleaned.json)
3. [data\clean\ShareGptChatPairs_2415_cleaned.json](data\clean\ShareGptChatPairs_2415_cleaned.json)

Cleaning data is covered in [\dev\clean_data.ipynb](\dev\clean_data.ipynb)


## 3. Install Everything
Assuming you have absolutely nothing

### VSCODE IDE
https://code.visualstudio.com/download 

Getting started with Jupyter in VSCOde
https://donjayamanne.github.io/pythonVSCodeDocs/docs/jupyter_getting-started/

Ctrl+Shit+P - Python
for handy python commands in vscode

#### VSCODE Extensions
These are the extensions I installed:

```
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
```

### Python
I prefer the lightweight miniconda installation:
https://docs.conda.io/en/latest/miniconda.html 


#### Install Project's Python Requirements
***requirements.txt*** contains the version of packages required to run the notebooks. From a CMD/PS/BASH prompt execute:
```
pip install -r requirements.txt
```


## 4. API Key Security!
FOr use in the notebooks, the API keys must be stored in the *.env* file. There is an *env* file containing variables without values. Rename it to .env (dot env) and add you API keys.  

Note that the entries in the .env file do not use whitespace or quotes:
```
NOMIC_API_KEY=xjTljhsdfjhIuhBIIJBASDx_
COHERE_API_KEY=uhBIIJabcasd1234kjASFkjfjhIBASDx_
```

The .gitignore file contins this an ignore entry for your dot env file:
```
# api keys
.env
```

No need to use real environment variables. The API Keys are loaded using *load_dotenv*: 
```python
import os
from dotenv import load_dotenv
load_dotenv()
api_key = os.getenv('NOMIC_API_KEY')
```

Get your api keys from the URLs in # 5, below

## 5. Vector Database Setup
The Vector database space is moving insanely fast. I've found that most of the startups don't have time or resources to keep their docs or tutorials up to date.

I chose Weaviate because it's a very easy-to-work-with vector db. I tried several of the usual suspects but found that Weaviate tutorials worked first time and the documentation is complete enough.

The feature I like the most is the ability to create a schema with any properties or fields that are needed, and choose which fields will be vectorized.

Weaviate was also easy to use via docker. There's also a free to try cloud version.  

#### Weaviate on docker
You can generate a new docker-compose.yml or use the one provided in this project.

Make sure you have docker engine and docker-compose installed and in your PATH.
https://www.docker.com/products/docker-desktop/ 

Weaviate has a docker-compose configuration tool on their site: 
https://weaviate.io/developers/weaviate/installation/docker-compose

I have included my [docker-compose.yml](docker-compose.yml) 

After you run the Weaviate contaier, check it's working with http://localhost:8080/

### Weaviate connection error
If you get this error
>error getting credentials - err: exec: "docker-credential-desktop": executable file not found in %PATH%, out: ``

Edit the {user}\.docker\config.json and remove the line as shown:

```json
{
  "credsStore": "desktop" <- DELETE THIS LINE
}
```

### Sentence Transformers
Sentence transformers are the OG. History and explanation available here:
https://towardsdatascience.com/attention-is-all-you-need-discovering-the-transformer-paper-73e5ff5e0634

More information about them can be found here: https://www.sbert.net/ and here: https://huggingface.co/sentence-transformers 

If you would like to try a different sentence transformer, look here: https://www.sbert.net/docs/pretrained_models.html

#### This project uses 'multi-qa-MiniLM-L6-cos-v1'
The sentence transformer chosen for this project is documented here
[sentence-transformers/multi-qa-MiniLM-L6-cos-v1](https://huggingface.co/sentence-transformers/multi-qa-MiniLM-L6-cos-v1) 

It maps sentences & paragraphs to a 384 dimensional dense vector space and was designed for semantic search. It has been trained on 215M (question, answer) pairs from diverse sources. For an introduction to semantic search, have a look at: SBERT.net - Semantic Search

| Description:              | This model was tuned for semantic search: Given a query/question, if can find relevant passages. It was trained on a large and diverse set of (question, answer) pairs. |
|---------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Base Model:               | nreimers/MiniLM-L6-H384-uncased                                                                                                                                         |
| Max Sequence Length:      | 512                                                                                                                                                                     |
| Dimensions:               | 384                                                                                                                                                                     |
| Normalized Embeddings:    | true                                                                                                                                                                    |
| Suitable Score Functions: | dot-product (util.dot_score), cosine-similarity (util.cos_sim), euclidean distance                                                                                      |
| Size:                     | 80 MB                                                                                                                                                                   |
| Pooling:                  | Mean Pooling                                                                                                                                                            |
| Training Data:            | 215M (question, answer) pairs from diverse sources.



### Vector DB Visual Exploration
Visualizing your sentence embedding vectors is powerful way of exploring your data. It's particularly helpful when you are creating a benchamrk sample set of promts for your use case.

This project uses free resources available from https://atlas.nomic.ai/

Click button labeled: Get Started with Atlas


### How to visualize weaviate data:
https://docs.nomic.ai/vector_database.html#weaviate

If you're not seeing the correct data in nomic atlas, 
go to https://atlas.nomic.ai/dashboard 
and check the list of projects and make sure you're looking at the right one.
You umay want to delete the existing indexes for a project.
I advise against deleting an entire project. That caused me some trouble...

implemented here: 
 1. [dev_nb\nomic.ipynb](dev_nb\nomic_start_here_dev.ipynb)
 1. [work_nb\drift_nomic.ipynb](work_nb\drift_nomic.ipynb)


## 6. Generative AI Account Setup
This project used a free API account at cohere.ai
Open https://cohere.com/ 
Click on Try Now button upper right corner.

### The Cohere Platform
https://docs.cohere.com/docs


## 7. SQLite
SQLite is used to store the time-series data generated when we run the benchmark sample every day or week or...

Setup is incredibly simple:
https://www.sqlite.org/index.html

### Create a project db
A SQLite3 DB (\data\driftDb.db) is included. However, if you want to create your own: 
https://www.sqlite.org/quickstart.html


## Confirm external resources are working:
Run the scripts in [confirm_external_resources.ipynb](confirm_external_resources.ipynb)


## Now that setup is complete:
    1. Learn and experiment by using the notebooks in the dev/ directory, or
    2. Get straight to work with the notebooks in the work/ directory.


  ***Have fun storming the castle!***