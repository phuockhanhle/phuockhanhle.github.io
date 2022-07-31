---
layout: post
title:  "Machine Learning Engineer Internship : keyword extraction research and intergration"
date:   2022-07-20 16:41:53 +0700
categories: jekyll update
---

## Abtract
At the end of my study at Université de technologie en Compiègne, I implemented the intership as a machine learning engineer. In this intership, I have opportunity to do the reseach and intergration of one of the feature of [Sinequa][sinequa] production : Keyword extraction. In the first phase, I gave my try on applying deep learning model to resolve the problem of keyword extraction. The main idea is to apply, reproduce the result, improve the performance of [Bert Joint KPE][Bert-joint-kpe]. I extended my research in applying model on long document which is weakness of [BERT base model][Bert]. In the next phase of my intership, I implemented the feature of keyword extraction in Sinequa's production, using the result of research part. After this phase, Sinequa application can use pretrained deep learning to run the task keyword extraction in all of its use-cases. This intership is a great opportunity for me to improve my deep learning research skills and integrate deep learning feature in production.
## Project description


## Data pipeline
Data is one of the most important element in a deep learning project. In order to get a generalized data, I collect data from various source and topic. However, as the model is a product for commercial, the source should be free for commercial. At the end, I conclude only 4 dataset : [inspec], [pubmed], [semeval17], and [kptimes]. There are also [ldkp10k] dataset which is in process to check validity. As each data's source have its own representation, I design a data pipeline to transform from raw format to input format of the model.

First of all, I determined a pivot format for the data. This is the common format for all dataset, and it contains only the information needed for training and evaluating keyword extraction. Hence, each sample in pivot contains : url as id of the document, document in initial format, and list of keyword or keyphrase. As I use a script for each dataset to transform from raw format to pivot format.

From pivot format, the data will pass preprocess to get input format. In the phase, we can choose different strategies for prerprocessing : tokenization, casing or uncasing, long document processing, stemmization or lemmization or not. Each strategy of preprocessing influences on performance of the model. Hence, I consider the preprocessing as a hyperprameter of the model. 

## Research Keyword extraction with Bert-Joint KPE

**Bert-Joint KPE** is a deep learning algorithm using bert base model to adapt on extracting keywords of a document. The [image] described the architechture of the model. First of all, the raw text is passed into a BERT model to extract one token embedding per token. It embeds each token of the document into a numeric vector that contains abstract information in the current context. There are various variants of Bert that have different features. The token embeddings are then fed into a custom CNN with various windows size (from 0 to the maximum length of a keyphrase) which will create an N-gram representation for every possible N-gram. Those N-gram representations are then fed to the chunking network, which will select which N-grams are keyphrases or “Chunks” thanks to a linear binary classification layer. Those chunks are in turn fed to the ranking network which will rank them according to their salience and assign a score to each of them with a linear layer. The training is made jointly on the combined loss of the chunking and ranking network: L = L_Chunk + L_Rank. For the L_Chunk, the cross-entropy is computed for every chunk where the chunk label is 1 if the chunk represents a keyphrase and 0 otherwise. For L_Chunk, the hinge loss in pairwise learning to rank is computed on exact matches with ground truth by minimizing the score of non-keyphrases minus the score of real keyphrases.

## Research Keyword extraction on long document
## Intergration keyword extraction in Sinequa production

[sinequa]: https://www.sinequa.com/?utm_source=google&utm_medium=cpc&utm_campaign=%7BCampaignName%7D&utm_content=%7BAdGroupName%7D&utm_term=Sinequa&gclid=Cj0KCQjwlemWBhDUARIsAFp1rLXEPxS0kbeV2lFqli6XioRSwsALfYZ7FOb1Ialzkj5_qq9wCmM75XEaApaGEALw_wcB
[Bert-joint-kpe]: https://arxiv.org/pdf/2004.13639.pdf
[Bert]: https://en.wikipedia.org/wiki/BERT_(language_model)


