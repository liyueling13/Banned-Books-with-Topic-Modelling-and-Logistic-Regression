# Predicting-Banned-Books-Using-Topic-Modelling-and-Logistic-Regression


![9781549304002](https://github.com/liyueling13/Predicting-Banned-Books/assets/81717153/b9fbebab-7cb6-4169-bab1-12b1098a293f) ![9781250756145](https://github.com/liyueling13/Predicting-Banned-Books/assets/81717153/bd47fd6f-3e69-4778-bd2d-6f3f734a6a4e) ![9780786851720](https://github.com/liyueling13/Predicting-Banned-Books/assets/81717153/681b2eb4-03e2-449f-b3e9-58c08b585179)

## Intro
Over July 1, 2021 to June 30, 2022, PEN America recorded **2531 book bans of 1656 unique books** in schools across America. 

What kinds of books are being censored? [According to PEN America](https://pen.org/banned-books-list-fall-2022/), popular themes for censorship are race, history, and gender and sexuality.

Is this in fact the case? Let's build a model that will predict whether a book will be banned, and what themes ("features") are relevant.

## Data
I sourced my banned books from PEN America ([spreadsheet here](https://docs.google.com/spreadsheets/d/1hTs_PB7KuTMBtNMESFEGuK-0abzhNxVv4tgpI5-iKe8/edit#gid=1171606318)). These book bans occurred from July 1, 2021 - June 30, 2022. Using BeautifulSoup, I scraped my non-banned books from a private blog, [Library of 1000 Books](https://libraryof1000books.wordpress.com/the-list-of-1000-books/), containing 1000 well-known books. I checked for overlap with the PEN America list and removed duplicates. These dataframes contained authors and titles.

Using the Google Books API, I pulled Book Descriptions for both spreadsheets (banned and well-known books). For example, the description for Daniel Aleman's Indivisible reads:
> A timely, moving debut novel about a teen's efforts to keep his family together after his parents are detained and deported. Mateo Garcia and his younger sister, Sophie, have been taught to fear one word for as long as they can remember: deportation. Over the past few years, however, the fear that their undocumented immigrant parents could be sent back to Mexico has started to fade. Ma and Pa have been in the United States for so long, they have American-born children, and they're hard workers and good neighbors. When Mateo returns from school one day to find that his parents have been taken by ICE, he realizes that his family's worst nightmare has become a reality. With his parents' fate and his own future hanging in the balance, Mateo must figure out who he is and what he is capable of, even as he's forced to question what it means to be an American. Daniel Aleman's Indivisible is a remarkable story -- both powerful in its explorations of immigration in America and deeply intimate in its portrait of a teen boy driven by his fierce, protective love for his parents and his sister.

I was not able to pull descriptions for all books, perhaps due to spelling errors or otherwise. I was left with a total of **1701 books**, **1013 of which were banned and 688 of which were not banned.**

I used Scattertext to create a visualization of nouns appearing in the descriptions of banned and non-banned books.

![Scattertext - Banned Books - Nouns](https://github.com/liyueling13/Predicting-Banned-Books/assets/81717153/a0cf84fd-3aa1-4d4c-b61a-fa91a4532c32)

[Scattertext - Interactive Visualization - will take some time to load](https://liyueling13.github.io/Banned%20Scattertext%20Explorer.html)

## Tools
1. Numpy and pandas for data wrangling
2. 

![PEN America Banned Books 2023](https://pen.org/wp-content/uploads/2023/04/Option-02%E2%80%94v2.png)
[Picture from PEN America's Banned Books Webpage](https://pen.org/report/banned-in-the-usa-state-laws-supercharge-book-suppression-in-schools/)

