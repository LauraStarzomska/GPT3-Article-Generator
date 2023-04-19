# BMW Project

* General info
* Technologies
* Files
* Steps
* Setup

## General info

The project's aim is to create article generator, model based on Artificial Intelligence. The generator would create press releases similar to BMW's ones. The model would read all bmw articles with headers and based on them, it will learn to create similar ones. In the end the user would introduce header/article's intro and generator would produce article's content. 

## Technologies

This project is created with:
* GPT-3 
* Webscraping using selenium and beautiful soup modules
*

## Files
* data - file with csv and xlsx scraped data
* codes - files with scraper and article generator

## Steps 

1. Scraping data
2. Cleaning data
3. Restructuring from csv/excel -> jsonl 
4. Fine-tuning model
5. Building article generator function.

## Setup

- Firstly, we have to gather data from [https://www.press.bmwgroup.com/global]. To do it, we write scraper using selenium and beautiful soup. The scraper can be found in codes folder and is named **'bmw_scraper.ipynb'** For selenium package, we need to download webdriver for chrome, unpack it and move it to your **/usr/local/bin** path. You can download webdriver from here: https://chromedriver.chromium.org/downloads the version of chromedriver is the same as your Google Chrome's one (can be checked in settings). 
We also have to clean our data. Getting rid of unneeded phrases, white spaces etc. At the end collected and cleaned data have to be saved in jsonl format as example:
```{"prompt": "<prompt text>", "completion": "<ideal generated text>"}```
for our case, if we want to generate articles based on article's intro/header then prompt would be intro/header and completion would be article'content. 
 - ### Fine-tuning
In order to improve our GPT-3 model, it's adviced to fine-tuned model which would make them more fault-immuned, faster. Fine-tuning improves on few-shot learning by training on many more examples than can fit in the prompt, letting you achieve better results on a wide number of tasks. Once a model has been fine-tuned, you won't need to provide examples in the prompt anymore. 
 - ### Preparing data for fine-tuning (jsonl format)
1. Open terminal
2. ```pip install --upgrade openai```
3. ```export OPENAI_API_KEY="<OPENAI_API_KEY>"```
OpenAI developed a tool which validates and formats data.
5. ```openai tools fine_tunes.prepare_data -f <LOCAL_FILE>```

Now, when we have our data ready, time to prepare model.
 - ### Preparing fine-tuned model
 1. Open terminal
 2. ```openai api fine_tunes.create -t <TRAIN_FILE_ID_OR_PATH> -m <BASE_MODEL>```
Base model can be one of: ada, babbage, curie, or davinci. The choice of model influences both the performance of the model and the cost of running your fine-tuned model. Read documentation to find more: [https://beta.openai.com/docs/models]
When run properly, on the end of the process you will get your model id which can be used in creating article generator.

- ### Writing BMW article generator
The file with BMW article generator that uses fine-tuned can be fined in codes folder and is named **bmw_article_generator.ipynb**
