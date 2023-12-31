# General knowledge on AI

## Federated Learning

Federated learningis a way to train multiple ML models on multiple dataset without exchange of samples of the dataset. In practice, one proceeds as follows. Consider K datasets. Train a model on each of the K dataset independently. Then Build a final model from the parameters of the K models. e.g. it trains a meta model on the parameters of the K model.

Advantage: there is no assumption of homogeneity or iid for the dataset. The size of the datasets can be very different.

source:
https://en.wikipedia.org/wiki/Federated_learning

https://arxiv.org/abs/2310.15165

https://arxiv.org/abs/1602.05629


## Complex Valued Neural Network:

https://machine-learning-made-simple.medium.com/complex-valued-neural-networks-might-be-the-future-of-deep-learning-c51f71f4c835


## Calibration

paper on the importance of calibration in sport betting prediction
https://arxiv.org/pdf/2303.06021.pdf


a way to measure how well calibrated a model is is the classwise-ECE (Expected Calibration Error)

The calibration is the notion that the probability of a classifier assigns to an event should reflect the true frequency of that event.

It is explained in this paper which introduces the dirichlet method, a method which calibrates better ML models

https://pypi.org/project/classifier-calibration/#:~:text=classwise_ece%20%28%29%20returns%20the%20classwise%20expected%20calibration%20error,expected%20rate%20of%20occurrence%20of%20the%20given%20class.

https://arxiv.org/pdf/1910.12656.pdf




# General Knowledge on NLP

## General LLM

https://jalammar.github.io/visualizing-neural-machine-translation-mechanics-of-seq2seq-models-with-attention/

https://docs.google.com/presentation/d/12sCcP2DsB1AvnHZ6YHMhS9KiKjbgH5P97kZRDBZkno4/edit#slide=id.p


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

## Seq2seq

a seq2seq model takes a sequence of items as input and outputs another sequence of items. In LLM, items are usually words. The model is composed of an **encoder** and a **decoder**.

### encoder-decoder-context

the **encoder** processes each item in the input sequence, it compiles the information it captures into a vector (called the **context**). After processing the entire input sequence, the **encoder** sends the **context** over to the **decoder**, which begins producing the output sequence item by item. 

The context is a vector (an array of number) and you can set its sizewhen you set up your model. It is typically the number of hidden units in the encoder RNN. The encoder and the decoder are both RNN. An RNN takes two input vectors: a hidden state and an input. the RNN outputs two vectors: an hidden state and an output.

We talk about time step in LLM, each time step corresponds to a word/item/token.

Note that the last hidden state of the encoder is te contxt that is passed to the decoder.

Attention is a technique that allows the models to deal with long sentences. It allows the models to focus on the relevant parts of the input sequence. Attention amlifies the important token of the input sequence.

### attention

look also at the jalammar github:
https://jalammar.github.io/visualizing-neural-machine-translation-mechanics-of-seq2seq-models-with-attention/

Attention models differe from classical sequence-to-sequence models in 2 main ways:
1. First the encoder passes a lot more data to the decoder, as it passes *all* thehidden states of the encoder to the decoder.
2. Second the decoder does an extra step before producing its output. It takes all the hidden states of the encoder (each of them being associated with 1 token) and processes a weighted averaged normalized of them, pthus producing a single context vector of the shape of a single hidden state. In order to do so it proceeds as followed:

    1. score each hidden state (i.e. assign a number to it)
    2. apply softmax to each score
    3. multiply each hidden state by the softmaxed score
    4. sum up the weighted vectors 

Now let's bring altogether:
1. The attention decoder RNN takes in the embedding of the <END> token and an initial decoder hidden state.
2. The RNN processes its inputs, producing an output and a *new hidden state* vector. The output is discarded.
3. Attention step: we use the encoder hidden states and the new hidden state vector to calculate a context vector for this time step.
4. We concatenate the new hidden state and the context vector into one vector.
5. We pass this vector through a feedforward neural network (one trained jointly with the model)
6. The output of the feedfoward neural networks indicates the output word of this time step.
7. Repeat for the next time steps

In fact I am not sure what you should use instead of the <END> token at the next time step? The output vector of the encoder RNN for the second time step? first time step? the token f the input sequence directly?


look at the papers:

https://proceedings.neurips.cc/paper_files/paper/2014/file/a14ac55a4f27472c5d894ec1c3c743d2-Paper.pdf

https://arxiv.org/abs/1406.1078

https://arxiv.org/abs/1409.1259


## Transformer

The big picture of a transformer is the following:

<img width="597" alt="transformer" src="https://github.com/cosmo-gb/Knowledge/assets/55383209/63a1e55f-9470-42f2-b599-2cafa37801e9">

In this example, you have 6 layers of encoder and 6 layers of decoder (the number 6 is arbitrary here). Each encoder is made of 2 sub-layers: the *feed forward* neural network and the *self-attention*, as shown here:

<img width="394" alt="encoder" src="https://github.com/cosmo-gb/Knowledge/assets/55383209/eeb60bd8-25c0-44e1-a552-24a499446f9e">

The role of the *self-attention* sub-layer is to push the model to pay attention to other words in the input sequence than the word (i.e. token) it is processing. The main difference between an encoder and a decoder is the presence of a encoder-decoder attention sub-layer in the decoder:

<img width="405" alt="encoder_decoder" src="https://github.com/cosmo-gb/Knowledge/assets/55383209/57900a14-a5b5-440a-af4e-a0ece092a1cb">

This encoder-decoder sub-layer helps the decoder focus on relevant parts of the input sequence.

### start with embedding

Before any computations, one needs to turn each input word/token into a vector using an *embedding algorithm*. This is the role of the bottom-most encoder (i.e. the first encoder). Each encoder receive a list of vectors each of the same size (e.g. 512). In the bottom encoder that would be the word embeddings, but in other encoders, it would be the output of the encoder that's directly below (i.e. the previous encoder). The size of this list of vector is a hyperparameter that we can set, it could be the length of the longest sentence in our training dataset. After embedding, the following occurs for the first encoder:

<img width="457" alt="encoder_1" src="https://github.com/cosmo-gb/Knowledge/assets/55383209/25cd4428-dab2-449b-94fb-ea95d5c669ff">

A very important property of transformers is that each word/token flows through its own path in the encoder. There are dependencies between these paths in the self-attention layer. The feed-forward layer does not have those dependencies. Thus the various paths can be executed in parallel while flowing through the feed-forward layer. Here is an example of what is happening between the first and the second encoder:

<img width="462" alt="encoder_2" src="https://github.com/cosmo-gb/Knowledge/assets/55383209/18b2c82e-0f2f-480f-bed4-5a07d71c4d09">

### self-attention in details

Self-attention mechanism can be splited in different steps:
1. the **first step** is to create a *Query, Key* and *Value* vector for each word/token. These 3 vectors are created by multiplying the input vectors (the embedding for the first encoder) by 3 matrices that are trained during the process. The dimension of these vectors can be smaller than the dimension of the embedding vector. In our example, the dimensionality of these 3 vectors is 64, while the dimension of the embedding and encoder input/output is 512. The query, key and value vectors are abstractions useful to the self-attention mechanism. <img width="445" alt="Queries_Keys_Values" src="https://github.com/cosmo-gb/Knowledge/assets/55383209/751841af-9328-4121-bb2f-72e08718e6fc">
2. the **second step** is to calculate a *score*. We need to score each word of the input sequence against each other. The score is computed with query and key vectors, as described as follows for the word thinking:
<img width="385" alt="score_computed" src="https://github.com/cosmo-gb/Knowledge/assets/55383209/46c19efc-3a2b-4517-8fda-e85a09d21884">
3. the **third step** is to compute the weighted sum of all the values, where the weight are the scores computed in the **second step**<img width="364" alt="weighted_sum" src="https://github.com/cosmo-gb/Knowledge/assets/55383209/8b922a94-3731-48d9-b46c-dff8f8c6dfab">
This concludes the self-attention mechanism. The resulting vector is the one we can send along to the feed-forward neural network. All these steps can be done in matrix form:

<img width="261" alt="QKV_matrices" src="https://github.com/cosmo-gb/Knowledge/assets/55383209/90fa5bee-9f99-45f3-9a15-1d03239e9c52">
<img width="328" alt="score_and_sum" src="https://github.com/cosmo-gb/Knowledge/assets/55383209/cc857844-d7fb-470f-bed3-219c268491dc">

One can refine the previous self-attention mechanism with **multi-headed self-attention**. In this case, one start with many matrices for Q, K and V with different initialization. This work as follows (this is an example with 8 heads) (x is the embedding vector, while r is the output vector of an encoder):

<img width="479" alt="multi_head_self_attention" src="https://github.com/cosmo-gb/Knowledge/assets/55383209/24255350-ffab-4e3d-a9b4-45b94e076f21">

### order in the sequence

### residuals

### decoder

### final linear and softmax layer

### loss function


annotation of Attention is all you need & pytorch:
http://nlp.seas.harvard.edu/2018/04/03/attention.html




## Attention

attention introduced:
https://arxiv.org/abs/1409.0473
https://arxiv.org/abs/1508.04025

Attention is all you need
Vaswani et al 2017
https://arxiv.org/abs/1706.03762

see also:
https://www.youtube.com/watch?v=fjJOgb-E41w

## Transformer

very detailed and clear:
https://jalammar.github.io/illustrated-transformer/

https://www.youtube.com/watch?v=iH-wmtxHunk

very good, derived from scratch from intuition of what we need:
https://www.youtube.com/watch?v=kWLed8o5M2Y


transformer from scratch:
https://levelup.gitconnected.com/understanding-transformers-from-start-to-end-a-step-by-step-math-example-16d4e64e6eb1



# how to stay update in AI

arxiv sanity preserver:
https://arxiv-sanity-lite.com/

arxiv:
https://arxiv.org/list/cs.AI/recent

marktechpost:
https://www.marktechpost.com/

ENX:
https://drive.google.com/drive/folders/0AGAmIKnK2WrTUk9PVA

