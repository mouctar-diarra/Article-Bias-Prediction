# Article-Bias-Prediction

## Overview
The goal of this repository is to evaluate the political bias of provided news articles and provide additional news articles of the same topic from across the political spectrum. The intention and purpose behind this code is to try to mimic the "blindspot" feature from https://ground.news/. 
This repository includes two Jupyter notebooks: 
* **News_Bias_Classification_Model** creates and trains a PyTorch classification model to classify political biases of news articles.
* **News_Bias_Indicator** applies the PyTorch classification model to classify the political bias of a provided article and provide similar/alternative coverage of the same news story.

## Dataset
The articles crawled from www.allsides.com are available in the ```./data``` folder, along with the different evaluation splits.

The dataset consists of a total of 37,554 articles. Each article is stored as a ```JSON``` object in the ```./data/jsons``` directory, and contains the following fields:
1. **ID**: an alphanumeric identifier.
2. **topic**: the topic being discussed in the article.
3. **source**: the name of the articles's source *(example: New York Times)*
4. **source_url**: the URL to the source's homepage *(example: www.nytimes.com)*
5. **url**: the link to the actual article.
6. **date**: the publication date of the article.
7. **authors**: a comma-separated list of the article's authors.
8. **title**: the article's title.
9. **content_original**: the original body of the article, as returned by the ```newspaper3k``` Python library.
10. **content**: the processed and tokenized content, which is used as input to the different models.
11. **bias_text**: the label of the political bias annotation of the article (left, center, or right).
12. **bias**: the numeric encoding of the political bias of the article (0, 1, or 2).

The ```./data/splits``` directory contains the two types of splits, as discussed in the paper: **random** and **media-based**. For each of these types, we provide the train, validation and test files that contains the articles' IDs belonging to each set, along with their numeric bias label.

The authors of the data explored the task of predicting the leading political ideology or bias of news articles in a 2020 research paper: https://aclanthology.org/2020.emnlp-main.404.pdf

## News_Bias_Classification_Model
This standalone notebook isn't required to be run to use the News Bias Indicator. Given the large dataset size, hyperparameter tuning can take several hours to complete. 
This notebook showcases the parameters and training behind the final pretrained classification model.

## News_Bias_Indicator
This standalone notebook uses Hugging Face Hub to host the pretrained classification model. In addition, it uses SerpAPI to query related news articles.
SerpAPI is required to fully utilize the "blindspot" functionality in this notebook. You can create an account for free at https://serpapi.com/ and recieve an API key.
Furthermore, several news sources have measures that prevent web scrapping. As a result, some input articles that you provide may not be extracted properly.

## Required Libraries & Modules
This repository contains Jupyter Notebook code that requires the following Python libraries. To run the notebooks successfully, please ensure all dependencies are installed.
For users with a standard Anaconda setup, most packages like `pandas`, `numpy`, `json`, `pathlib`, and `time` are included by default.  
For packages not included by default, you can install them using `pip` in a terminal or directly in a Jupyter Notebook cell:

pip install torch
pip install transformers
pip install itables
pip install fastparquet
pip install optuna
pip install lxml_html_clean
pip install selenium
pip install webdriver-manager
pip install google-search-results
