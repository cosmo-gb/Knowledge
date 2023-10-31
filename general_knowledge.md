# General knowledge on AI

## Federated Learning

Federated learningis a way to train multiple ML models on multiple dataset without exchange of samples of the dataset. In practice, one proceeds as follows. Consider K datasets. Train a model on each of the K dataset independently. Then Build a final model from the parameters of the K models. e.g. it trains a meta model on the parameters of the K model.

Advantage: there is no assumption of homogeneity or iid for the dataset. The size of the datasets can be very different.

source:
https://en.wikipedia.org/wiki/Federated_learning

https://arxiv.org/abs/2310.15165

https://arxiv.org/abs/1602.05629

## Calibration

paper on the importance of calibration in sport betting prediction
https://arxiv.org/pdf/2303.06021.pdf


a way to measure how well calibrated a model is is the classwise-ECE (Expected Calibration Error)

The calibration is the notion that the probability of a classifier assigns to an event should reflect the true frequency of that event.

It is explained in this paper which introduces the dirichlet method, a method which calibrates better ML models

https://pypi.org/project/classifier-calibration/#:~:text=classwise_ece%20%28%29%20returns%20the%20classwise%20expected%20calibration%20error,expected%20rate%20of%20occurrence%20of%20the%20given%20class.

https://arxiv.org/pdf/1910.12656.pdf




# General Knowledge on NLP

## distributional structure main core idea

Zellig Harris 1954, distributional structure

https://www.tandfonline.com/doi/epdf/10.1080/00437956.1954.11659520?needAccess=true

J.R. Firth 1957, book
https://books.google.be/books/about/A_Synopsis_of_Linguistic_Theory_1930_195.html?id=T8LDtgAACAAJ&redir_esc=y

## vector space models of semantics

review: Turney and Pantel, 2010
https://arxiv.org/abs/1003.1141

3 types of VSM:
1. **term-document**: 
terms can be words and documents can documents, webpages, books, ...
the term-document matrix is made of *n* rows (*n* is the number of terms) and *m* columns (*m* is the number of documents), the element *i*,*j* of the matrix representing how many times the term *i* is present inside the document *j*. We call a bag the list of terms in a document i.e. represents a document. You can have duplicates in a bag and the order does not count in a bag. Mathematically, a bag is a multiset (a set with duplicates). Here the goal is to find similarities between document. Then one can use this matrix to ask queries that can be treated as pseudo-document and find which document is the most similar to the query. This document would be the document which best answer to the query. The term-document matrix is deeply related to the  the *bag of words hypothesis* which states that we can estimate the relevance of documents to a query by representing the documents and the
query as bags of words.
2. **word-context**:
it is similar to term-document, but here the focus is on the term not on the document (i.e. we want to find similarities between words and not similarities between documents) and the documents are replaced by context which can be either words, phrases, sentences, paragraphs, chapters, documents, grammatical dependencies, ... The word-context is deeply related to the *distributional hypothesis* which states that words that occur in similar contexts tend to have similar meanings (see Harris 1954, Wittgenstein 1953).
3. **pair-pattern**: the rows are pairs of words (e.g. carpenter:wood) and the columns are patterns i.e. relations between pairs of words (e.g. X cuts Y)

There are different kind of similarities: attributional similarity (e.g. synonyms and antonyms), relation similarity (between pair of words e.g. cat:meow and dog:bark)

**token**: single instance of a symbol/word
**type**: general class of token
    

## word representation in vector space

Mikolov, Chen, Corrado & Dean 2013
https://arxiv.org/abs/1301.3781

## Attention

Attention is all you need
Vaswani et al 2017
https://arxiv.org/abs/1706.03762


# how to stay update in AI

arxiv sanity preserver:
https://arxiv-sanity-lite.com/

arxiv:
https://arxiv.org/list/cs.AI/recent

marktechpost:
https://www.marktechpost.com/
