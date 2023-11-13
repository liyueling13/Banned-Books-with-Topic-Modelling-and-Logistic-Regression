# Predicting-Banned-Books-Using-Topic-Modelling-and-Logistic-Regression

![9781549304002](https://github.com/liyueling13/Predicting-Banned-Books/assets/81717153/b9fbebab-7cb6-4169-bab1-12b1098a293f) ![9781250756145](https://github.com/liyueling13/Predicting-Banned-Books/assets/81717153/bd47fd6f-3e69-4778-bd2d-6f3f734a6a4e) 

[Pictures from PEN America's Banned Books Webpage](https://pen.org/report/banned-in-the-usa-state-laws-supercharge-book-suppression-in-schools/)

## Intro
Over July 1, 2021 to June 30, 2022, PEN America recorded **2531 book bans of 1656 unique books** in schools across America. [According to PEN America](https://pen.org/banned-books-list-fall-2022/), popular themes for censorship are race, history, and gender and sexuality. Is this in fact the case? Let's build a model that will predict whether a book will be banned, and what themes ("features") are relevant.

## Data
- I sourced my banned books from PEN America ([spreadsheet here](https://docs.google.com/spreadsheets/d/1hTs_PB7KuTMBtNMESFEGuK-0abzhNxVv4tgpI5-iKe8/edit#gid=1171606318)). These book bans occurred from July 1, 2021 - June 30, 2022.
- Using BeautifulSoup, I scraped my non-banned books from a private blog, [Library of 1000 Books](https://libraryof1000books.wordpress.com/the-list-of-1000-books/), containing 1000 well-known books. I checked for overlap with the PEN America list and removed duplicates. These dataframes contained authors and titles.
- Using the Google Books API, I pulled Book Descriptions for both spreadsheets (banned and well-known books). I was not able to pull descriptions for all books, perhaps due to spelling errors or otherwise.
- I was left with a total of **1701 books**, **1013 of which were banned and 688 of which were not banned.**

## Tools
1. Numpy and pandas for data wrangling
2. requests and BeautifulSoup for web scraping
3. Google Books API for obtaining book descriptions
4. matplotlib, seaborn, and Scattertext for data visualization and analysis
5. NLTK for NLP analysis (stopwords, tokenization, lemmatization, and more)
6. CountVectorizer and TFIDF for vectorizing words, and TruncatedSVD and NMF for topic modelling
7. sklearn for modelling and evaluation

## EDA
I used Scattertext to create a visualization of nouns appearing in the descriptions of banned and non-banned books.

![Scattertext - Banned Books - Nouns](https://github.com/liyueling13/Predicting-Banned-Books/assets/81717153/a0cf84fd-3aa1-4d4c-b61a-fa91a4532c32)

[Scattertext - Interactive Visualization - will take some time to load](https://liyueling13.github.io/Banned%20Scattertext%20Nouns.html)

## Modelling and Results
![Banned_Logreg_Coefficients](https://github.com/liyueling13/Predicting-Banned-Books/assets/81717153/c960fd29-0f8f-41f0-879c-e9262c0c4406)


