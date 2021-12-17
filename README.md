# !#$@: An obscene journey through quotations in media
## Abstract
The perception and use of profanity depend on the situation and differ from person to person. While swearing is relatively common and sometimes even welcomed in a relaxed environment, the use of such language is mostly frowned upon in a workplace or public spaces. This is why we are not likely to encounter it while reading the news. Still, heated debates and unexpected events can inspire the appearance of obscene language even in more formal settings. To better understand the circumstances in which profanity appears in media, we will explore Quotebank, a large and heterogeneous dataset of quotes from media. We will focus mainly on obscene quotes identified by a machine learning model. Our main goal is to analyze the distribution of such quotations through time and to examine their presence with respect to the attributes of the speakers who uttered them and the media outlets who featured those speakers.

## Research questions
1.  What is the overall distribution of obscene quotes?
2.  How does the use of profanity behave through time? Can we relate the use of profanity to certain events?
3.  Which speakers and groups of speakers are most likely to use obscene language? Are there any differences in the distribution of profanity with respect to the occupation or gender of a speaker?
4.  Which media sources feature vulgar speakers? How does it relate to the nature of the sources and their role? Which media sources censor profanities?
5.  What are profanities about? Which lexical categories are most represented in the profane quotations?

## Additional datasets
To obtain attributes of the speakers we will use the `speaker_attributes.parquet` dataset prepared by the teaching staff. The speaker attributes were obtained from [WikiData](https://www.wikidata.org/wiki/Wikidata:Main_Page).

## Methods

### Data processing
Due to the size of the data, it is not possible to load it entirely in memory, which is why we will mostly use [PySpark](http://spark.apache.org/docs/latest/api/python/) for data processing. The aggregated results that we obtain with spark will then be converted to Pandas dataframe so that they can be visualized.
### Identifying quotes with profanity
To identify obscene quotes, we use a combination of approaches. Firstly, we will employ an SVM-based machine learning model [profanity_check](https://pypi.org/project/alt-profanity-check/) to compute profanity scores (a real number between 0 and 1). Although the author reports high results on the Wikipedia comments dataset, we don't know a thing about its performance on Quotebank. Thus, we label as profanities only the quotations with a profanity score higher than 0.9. Aside from that, since some censored quotes may be difficult to handle for our model, we use regular expressions to identify and remove censorship from the quotes, labeling all the censored quotations as profane. Finally, since we opted for a high profanity score threshold, we missed quite a few true positives. To alleviate this we then use a large list of profane words from which we first select the words with a profanity_check's profanity score higher than 0.5, and then further filter the set manually.
### Empath
We also compute Empath's lexical categories and analyze them with respect to profane and non-profane quotes. 
### Analyzing speaker attributes and quote profanity
To analyze the profanity distribution of quotes with respect to speaker demographics, we will use data visualization techniques such as bar plots accompanied with confidence intervals. We use confidence intervals to argue that the differences in average profanity across different occupations or genders are statistically significant.

## Proposed timeline
**Week 1**: Develop the regular expression for removing censorship from the data, data cleaning  
**Week 2**: Assign sentiment and profanity scores to all the quotes in the data  
**Week 3**: Expand the initial analysis on the entire dataset, explore the relationship between sentiment and profanity, visualize the data, answer the research questions  
**Week 4**: Refine the plots, learn how to use GitHub pages, start with the data story  
**Week 5**: Finish the data story  

## Organization within the team
**Week 1**: Dani and Marko work on data cleaning and developing the regular expression while Dewmini and Mauro start working on homework 2.  
**Week 2**: Everybody works on the homework. In the meantime, we run the code for computing sentiment and profanity scores on the entire data.  
**Week 3**: Dewmini and Dani work on speaker-level analysis, Mauro analyzes profanity with respect to news outlets, while Marko explores the relations between sentiment and profanity in the quotes.  
**Week 4**: The team firstly meets to discuss potential improvements of the plots, develop the outline of the data story and select the GitHub Pages theme. We then split into two pairs. Dewmini and Marko work on the story aspect while Dani and Mauro work on visual appearance.  
**Week 5**: Everyone works on refining the data story.

## Who did what
Dani:
Dewmini:
Marko: Data preprocessing, temporal analysis, news outlet analysis
Mauro:

