# !#$@: An obscene journey through quotations in media
## Abstract
The perception and use of profanity depends on the situation and differs from person to person. While swearing is relatively common and sometimes even welcomed in a relaxed environment, the use of such language is mostly frowned upon in a workplace or public spaces. This is why we are not likely to encounter it while reading the news. Still, heated debates and unexpected events can inspire the appearance of obscene language even in more formal settings. To better understand the presence of profanity in media, we will explore Quotebank, a large and heterogeneous dataset of quotes from media. We will focus mainly on obscene quotes identified by a machine learning model. Our main goal is to analyze the distribution of such quotations through time and to examine their presence with respect to the attributes of the speakers who uttered them and the media outlets who featured those speakers.
## Research questions
1.  What is the overall distribution of obscene quotes?
2.  How does the use of profanity behave through time? Can we relate the use of profanity to certain events?
3.  Which speakers and groups of speakers are most likely to use obscene language? Are there any differences in the distribution of profanity with respect to occupation, gender or age of the speaker?
4.  Which media sources feature vulgar speakers? How does it relate to the nature of the sources and their role?
5.  Are there differences in the sentiment of obscene quotes?
## Additional datasets
1. To obtain attributes of the speakers we will use the `speaker_attributes.parquet` dataset prepared by the teaching staff.
## Methods
### Data processing
Due to size of the data, it is not possible to load it entirely in memory, which is why we will mostly use [PySpark](http://spark.apache.org/docs/latest/api/python/) for data processing.
### Identifying quotes with profanity
To identify obscene quotes, we will use [profanity_check](https://pypi.org/project/alt-profanity-check/). This tool is based on an SVM model. It takes a list of strings as an input and otputs the probability that the string is obscene. In this case, we have observed that applying the tool to the quotations using PySpark is not feasible because profanity_check is then applied on one row at a time. The tool works way faster when applied to a larger list of strings, which is why in this case we opt for assigning the profanity scores on larger chunks so we use Pandas for that purpose.
### Removing censorship
In the news swearwords are often censored (mostly by leaving only the first letter of a swearword and replacing the rest with asterisks or dashes), which can lead to decrease in recall of profanity classifier. Because of this we will use regular expressions to remove censorship from often censored words.
### Sentiment analysis
To assign sentiment scores to each quotation we will mainly use sentiment_analyzer implemented as a part of SparkNLP library.  Furthermore we aim to perform regressional analysis between sentiment of the quote and its profanity probability. For this we will use statsmodels. Aside from SparkNLP, we will experiment with EMPATH and AFFIN lexicons.
## Proposed timeline
1. **Week 1** : Develop the regular expression for removing censorship from the data
2. **Week 2**: Assign sentiment and profanity scores to all the quotes in the data
3. **Week 3**: Expand the initial analysis on the entire dataset, visualize the data, answer the research questions,
4. **Week 4**: Refine the plots, learn how to use GitHub pages, profanity literature research
5. **Week 5**: Develop the data story
## Organization within the team

