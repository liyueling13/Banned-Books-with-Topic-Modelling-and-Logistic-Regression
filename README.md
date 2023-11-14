# Predicting-Banned-Books-Using-Topic-Modelling-and-Logistic-Regression

![9781549304002](https://github.com/liyueling13/Predicting-Banned-Books/assets/81717153/b9fbebab-7cb6-4169-bab1-12b1098a293f) ![9781250756145](https://github.com/liyueling13/Predicting-Banned-Books/assets/81717153/bd47fd6f-3e69-4778-bd2d-6f3f734a6a4e) 

[Pictures from PEN America's Banned Books Webpage](https://pen.org/report/banned-in-the-usa-state-laws-supercharge-book-suppression-in-schools/)

## Intro
Over July 1, 2021 to June 30, 2022, PEN America recorded **2531 book bans of 1656 unique books** in schools across America. [According to PEN America](https://pen.org/banned-books-list-fall-2022/), popular themes for censorship are race, history, and gender and sexuality. Is this in fact the case? Let's build a model that will predict whether a book will be banned, and what themes ("features") are relevant.

## Data
- I sourced my banned books from PEN America ([spreadsheet here](https://docs.google.com/spreadsheets/d/1hTs_PB7KuTMBtNMESFEGuK-0abzhNxVv4tgpI5-iKe8/edit#gid=1171606318)). These book bans occurred from July 1, 2021 - June 30, 2022. I retained information about authors and titles.
- Using BeautifulSoup, I scraped my non-banned books from a private blog, [Library of 1000 Books](https://libraryof1000books.wordpress.com/the-list-of-1000-books/), containing 1000 well-known books. I checked for overlap with the PEN America list and removed duplicates. I retained authors and titles.
- Using the Google Books API, I pulled Book Descriptions for both spreadsheets (banned and well-known books). I was not able to pull descriptions for all books, perhaps due to spelling errors or otherwise.
- After cleaning, I was left with a total of **1477 books**, **938 of which were banned and 539 of which were not banned.**

## Tools
1. Numpy and pandas for data wrangling
2. requests and BeautifulSoup for web scraping
3. Google Books API for obtaining book descriptions
4. matplotlib, seaborn, and Scattertext for data visualization and analysis
5. NLTK and spacy for NLP analysis (stopwords, tokenization, lemmatization, and more)
6. CountVectorizer and TFIDF for vectorizing words, and TruncatedSVD and NMF for topic modelling
7. sklearn for modelling and evaluation

## Data Wrangling and EDA
I cleaned my data ("Book Descriptions") using various NLP techniques:
- removed stopwords
- removed all words except nouns and adjectives
- lemmatized words
- removed descriptions with too few words, truncated descriptions with too many

I used Scattertext to create a visualization of nouns and adjectives appearing in the descriptions of banned and non-banned books.

![Banned Scattertext Explorer](https://github.com/liyueling13/Predicting-Banned-Books/assets/81717153/19190299-7cce-44a3-acbc-0589f96a9e81)

[Scattertext Explorer - Interactive Visualization - will take some time to load](https://liyueling13.github.io/Banned%20Scattertext%20Explorer.html)

## Modelling and Results
I performed topic modelling to create "features" for my book descriptions. In the end vectorizing with TFIDF and singular value decomposition with NMF created the most descriptive columns:

![NMF top fourteen](https://github.com/liyueling13/Predicting-Banned-Books/assets/81717153/c7b01af0-7606-44da-98ed-d4b4ff916be2)

I described these topics with the following feature names:
1. "nyt_author"
2. "middle_and_high_school"
3. "award_winning_childrens"
4. "gender_and_sexuality"
5. "families_and_home"
6. "race_and_america"
7. "growing_up"
8. "young_woman_meets_man"
9. "classics"
10. "boy_girl_story"
11. "book_series"
12. "lgbtq_sexuality"
13. "friendship"
14. "prize_novel"

Using these features, I tried a few models: Logistic Regression, KNN, Decision Tree, and Random Forest. They performed about equally, so for maximum interpretability I stuck with Logistic Regression. It gave me about 78% accuracy on the test set (an improvement from 63% with the dummy classifier). Our parameters were penalty = l2, C = 0.1, solver = lbfgs, class_weights = balanced.

As we can see from both the graphs below, the books that are least likely to be banned seem to be Book Series (fantasy, war, etc.) and Classics. From the Logistic Regression coefficients, the books that are more likely to be banned include books about middle and high school experiences, followed closely by books about gender and sexuality, lgbtq issues, friendship, romance, and children's books.

![Banned_Logreg_Coefficients(1)](https://github.com/liyueling13/Predicting-Banned-Books/assets/81717153/57131c1b-c328-41c3-b75e-c1272393eb8c)
![Banned_KNN_Coefficients](https://github.com/liyueling13/Predicting-Banned-Books/assets/81717153/999f7c90-7344-483c-a371-2512325c9113)

## Future Steps
1. I'd like to scrape more data for non-banned books. Right now I am on the edge of imbalanced data (about 60% banned/40% non-banned). In particular I would like to source more books from elementary, middle, and high school libraries (rather than 1000 popular books in general). Some possible sources include the American Library Association (ALA) and the Association of Library Services for Children's (ALSC) summer reading lists, and the Battle of the Books (national and NC) reading lists. However, scraping these would require quite a bit of data wrangling as they're embedded in multiple webpages and/or pdfs.
2. I performed my topic modelling manually. I wonder: is there a more systematic way to find the best # of topics when working with singular value decomposition for NLP? Or perhaps this is a place for interpretation and judgment.
3. Ideally I would get my model to 80% accuracy. I think that having more data (closer to 1000 banned books/1000 non-banned books) would certainly help with this goal.
