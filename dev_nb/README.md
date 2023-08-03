# Generative AI - Issue & Observability 


### Confirm external resources are working:
Run the scripts in [data\confirm_external_resources.ipynb](data\confirm_external_resources.ipynb)


### dev notebooks in dev_nb directory
All of the dev notebook files end with _dev.ipynb
These are files I wrote while developing this project. 
You may them useful 

### Data in data directory
Please see the [LICENSE](LICENSE) file (Apache 2.0)

You need clean data when you send it to the gen ai API or import into your vector database.
There are two data directories:
1. [data\clean\](data\clean\)
2. [data\raw\](data\raw\)


### Data: raw or cleaned & formatted
There are three files with cleaned data, suitable fo use during development
The number in the file name is the number of json objects (chat pairs) in each file.

1. [data\clean\ShareGptChatPairs_2_clean_fmt.json](data\clean\ShareGptChatPairs_2_clean_fmt.json)
2. [data\clean\ShareGptChatPairs_dev_10_cleaned.json](data\clean\ShareGptChatPairs_dev_10_cleaned.json)
3. [data\clean\ShareGptChatPairs_2415_cleaned.json](data\clean\ShareGptChatPairs_2415_cleaned.json)

Cleaning data is covered in [\dev\clean_data.ipynb](\dev\clean_data.ipynb)


## DEV NOTEBOOKS


### Start with cleaning raw data with spaCy
https://spacy.io/ 
https://spacy.io/api/top-level 

Start by trying out the scripts in [dev_nb\spacy_sentence_to_tokens_dev.ipynb](dev_nb\spacy_sentence_to_tokens_dev.ipynb).
This will show you how spaCy works. 

N.B. Note the use of spacy.prefer_gpu()
Will it make a difference in processing time?

Then run the scripts in [dev_nb\spacy_sentence_to_tokens_dev.ipynb](dev_nb\spacy_sentence_to_tokens_dev.ipynb)
This will show you the spacy functions I have used to clean the chat prompts and completions data in the \data\raw directory.

Once you're ready, you can get to work and clean and format the data!
[work_nb\clean_data.ipynb](work_nb\clean_data.ipynb)



### TRY OUT NOMIC ATLAS
Atlas integrates with your workflow by organizing text, embedding datasets and creating interactive maps that can be explored in a web browser.

1. Make sure you get your login key
1. Make sure you have added the nomic login key to the .env file
1. Then run the code in dev_nb\nomic_start_here_dev.ipynb



### CHECK THE COHERE API
1. Make sure you get your login key
1. Make sure you have added the nomic login key to the .env file
1. Then run the code in dev_nb\cohere_dev.ipynb


### DOES SQLITE WORK?
A few quick examples of sqlite: 
[dev_nb\sqlite_db_dev.ipynb](dev_nb\sqlite_db_dev.ipynb)


#### Cleanup the db: 
[dev_nb\sqlite_drop_all_tables.ipynb](dev_nb\sqlite_drop_all_tables.ipynb)


## NOTEBOOKS

Once weaviate, cohere, sqlite and nomic are working, the work notebooks will take you from raw data to your first set of benchmark sample data.

*Start small*
If you're using a free completion API account, it's probably wise to not use up all your credits.

Work with the small raw & cleaned datasets until you're sure you want to spend money on a paid account.


## Steps:

0. [Delete out the old data in weaviate and sqlite](work_nb\00_clean_weaviate_and_sqlite.ipynb)
1. [Clean and format the raw data](work_nb\01_clean_data.ipynb)
2. [Import clean data to weaviate](work_nb\02_drift_benchmark_import.ipynb)
3. [Run the benchmark queries](work_nb\03_drift_benchmark_queries.ipynb)
4. [Visualize and explore the benchmark data in a browser](work_nb\04_drift_nomic.ipynb)


### Weaviate connection error
error getting credentials - err: exec: "docker-credential-desktop": executable file not found in %PATH%, out: ``

Edit {user}\.docker\config.json

```json
{
  "credsStore": "desktop" <- DELETE THIS LINE
}
```




