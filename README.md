============================================================================

TOXIC COMMENT CLASSIFICATION CHALLENGE (Jan 2018-March 2018)(Top 12 %)

============================================================================


--------------------------------------------------------------------------
Problem Description :->

src:(https://www.kaggle.com/c/jigsaw-toxic-comment-classification-challenge)

Discussing things you care about can be difficult. The threat of abuse and
harassment online means that many people stop expressing themselves and give
up on seeking different opinions. Platforms struggle to effectively 
facilitate conversations, leading many communities to limit or completely 
shut down user comments.
The Conversation AI team, a research initiative founded by Jigsaw and Google
(both a part of Alphabet) are working on tools to help improve online
conversation. One area of focus is the study of negative online behaviors, 
like toxic comments (i.e. comments that are rude, disrespectful or otherwise
likely to make someone leave a discussion). So far they’ve built a range of
publicly available models served through the Perspective API, including 
toxicity. But the current models still make errors, and they don’t allow 
users to select which types of toxicity they’re interested in finding (e.g. 
some platforms may be fine with profanity, but not with other types of toxic
content).

In this competition, you’re challenged to build a multi-headed model that’s 
capable of detecting different types of of toxicity like threats, obscenity,
insults, and identity-based hate better than Perspective’s current models. 
You’ll be using a dataset of comments from Wikipedia’s talk page edits. 
Improvements to the current model will hopefully help online discussion 
become more productive and respectful.

Disclaimer: the dataset for this competition contains text that may be 
considered profane, vulgar, or offensive.

Evaluation Metric : ROC - AUC (columns wise average)


--------------------------------------------------------------------------
EDA (Exploratory Data Analysis) :->

Comments were tagged into six categories namely toxic, severe_toxic, insult,
threat, obscene and identity_hate. There were no missing values at all but
class was higly imbalanced. Specially some classes like severe_toxic, threat,
identity_hate was highly imabalanced compared to total clean data. 
Another thing was that this problem was multilabel-multiclass tagging problem
So, some cases have even all tags but very rare(6 cases) but some cases have
more than two tags. Some comments consists of ip address too, so we need to
spend some time on text cleaning.
Some comments were too long as they were repeateadly written.

--------------------------------------------------------------------------
Preprocessing :->

Cleaning Phase :
>lowercasing
>Stopwords removal as they do not contain relevant information.
>Punctuation removal
>Stemming to prohibit repeated words in different forms
>remove special symbols
>clean extra spaces as there were some extra spaces in some cases

Feature Extraction:
>CountVectorizer : matrix with frequency counts of each word in the corpus
>TF-IDF Vectorizer : Penalizes words that are too frequent (regularization).
>HashingVectorizer : faster for larger text coprus
>no_of_words,avg_no_of_words,length_of_comment,no_of_upercase/lowercase/ratio
>no_of_punctutaions,no_of_special_chars


--------------------------------------------------------------------------
Modeling :->

First I tried with LogisticRegression linear model and it gave me a good
baseline. Now since most of the features were count based so it's obviuos
to try out multinomial naive bayes model, so I train with it but still
LogisticRegression was good. Now I used RandomForestClassifier and it
outperformed the previous linear models. Through using some varied sets
of parameters, I train several RandomForest, ExtraTrees, LogisticRegression
and XGBoost classifers, and lastly I blend all of their predictions.


--------------------------------------------------------------------------
Conclusion:
Linear Models may outperform complex models so, start with linear models.
Averaging works quite well in correcting errors so use it always.
