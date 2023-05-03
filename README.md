# Reproducibility Project for CS598 DL4H in Spring 2023

Matthew Lopes and Chris Kabat

{mlopes2, cjkabat2}@illinois.edu

Group ID: 59

Paper ID: 156

Presentation link: TBD


# Introduction

The paper we have chosen for the reproducibility project is:
Ensembling Classical Machine Learning and Deep Learning Approaches for Morbidity Identification from Clinical Notes (Kumar, V., Recupero, D. R., Rbioni, D., & Helaoui, R., 2021, 7197-7126)

The main goal of the paper is to extract co-morbidity recognition from clinical notes.  The idea was to use a combination of classical (CML) and deep learning methods (DML) to determine the best approach for classifying these notes in one or more of 16 morbidity conditions.  These models used a combination of NLP techniques including embeddings and bag of words implementations to provide input into the models.  It also measured the effect of including and removing stop words.  Lastly, it used ensemble techniques to tie together a number of the classical and deep learning models to provide the most accurate results.

The goal of our reproducibility study is to confirm the claims made in the paper as well as show how some additional techniques can be used to improve results.

## Methodology

In reproducing the research paper, we did not use any of the author's code as it was not provided in the paper. We aimed to follow the authors description of steps they took to get the results. The resources we used to reproduce this paper was the paper itself as well as some of the references from the paper. 
The paper did not share information about the hyperparameters used or how the Deep Learning models were constructed (although we inferred they were using Keras instead of Pytorch based on the description of the models).  We used hyper parameter sweeps (described below) to get the results as close as possible.

The following steps were taken to perform the study:

- Data Preperation
    - Downloaded the XML data from the N2C2 Obesity Challenge (n2c2, n.d.) and converted it from XML into dataframes.
    - Performed preprocessing steps such as Lemmatization, removal of punctuation, lower casing, removal of numbers, etc.
    - Tokenized in a word or sentence format
- Create Word Embeddings
    - Break large documents into multiple documents
    - Tokenize and pad the documents (words and sentences)
    - Test the embedding process
- Create OpenAI Embeddings
    - Call Open AI service and store embedding vectors for usage
- Run classical machine learning models
    - Run TF-IDF with feature selection
    - Run Embeddings
- Run deep machine learning models
    - Run TF-IDF with feature selection (BiLSTM)
    - Run Embeddings (BiLSTM)
- Run ensemble models
    - Run single ensemble model using the most effective CML and DL models

## Notebooks

The following notebook was used to prepare the dataset for use in the reproducability study:

[Data Preperation](https://github.com/chriskabat63/CS598FinalProject/blob/main/Project%20Workbook%20Data%20Preparation%20-%20156.ipynb)

The following notebook was used to create the word/sentence embeddings based on the text of the clinical notes:

[Create Embeddings](https://github.com/chriskabat63/CS598FinalProject/blob/main/Project%20Workbook%20Create%20Embeddings%20-%20156.ipynb)

The following notebook was used to pull sentence embeddings using Microsoft's Azure OpenAI cognitive service:

[Open AI](https://github.com/chriskabat63/CS598FinalProject/blob/main/Project%20Workbook%20OpenAI%20-%20156.ipynb)

The following notebook was used to execute all of the classical machine learning models:

[Classical ML Models](https://github.com/chriskabat63/CS598FinalProject/blob/main/Project%20Workbook%20Classical%20ML%20Models%20-%20156.ipynb)

The following notebook was used to execute all of the deep learning machine learning models:

[Deep Learning Models](https://github.com/chriskabat63/CS598FinalProject/blob/main/Project%20Workbook%20Deep%20Learning%20ML%20Models%20-%20156.ipynb)

The following notebook was used to execute the ensemble model we created as part of the study:

[Ensemble Models](https://github.com/chriskabat63/CS598FinalProject/blob/main/Project%20Workbook%20Ensemble%20Models%20-%20156.ipynb)

The following notebook was used to rename our final models once selected to simplify the ensemble process:

[Utilities](https://github.com/chriskabat63/CS598FinalProject/blob/main/Utilities.ipynb)

## Parameter Tuning

Because of the flexibility of the deep learning models we had a number of parameters we could change that could effect the results of the model.  We performed hyperparameter sweeps for a single morbidity condition by varying the following parameters:

- Epoch
- Batch Size
- Hidden State
- Drop Out
- Learning Rate

### DL Model for TF-IDF/Asthma

Here is a graphical representation of the effects of the parameters on the F1-MICRO scores:
![HP TFIDF](https://github.com/chriskabat63/CS598FinalProject/blob/main/images/HP-TFIDF.png?raw=true)

As a result we selected these parameters:

Feature | Batch Size | Dropout | Hidden State | Learning Rate | Epochs
---|---|---|---|---|---
All | 32 | 0.1 | 64 | 0.001 | 20
InfoGain | 32 | 0.1 | 64 | 0.01 | 40
ExtraTreesClassifier | 32 | 0.1 | 64 | 0.01 | 60
SelectKBest | 32 | 0.1 | 64 | 0.01 | 40

Note:  After many iterations of parameter sweeps, we made a couple generalizations that helped us get to our parameters:

* Processing with all features did best with a fewer number of epochs and lower learning rate
* ExtraTreesClassifier for feature selection benefited from more epochs

### DL Model for Embedding/Asthma

Here is a graphical representation of the effects of the parameters on the F1-MICRO scores:
![HP TFIDF](https://github.com/chriskabat63/CS598FinalProject/blob/main/images/HP-DL.png?raw=true)

As a result we selected these parameters:

Feature | Batch Size | Dropout | Hidden State | Learning Rate | Epochs
---|---|---|---|---|---
AOAI | 32 | 0.1 | 128 | 0.01 | 50
USE | 32 | 0.1 | 128 | 0.01 | 50
GloVe | 32 | 0.1 | 128 | 0.01 | 25
FastText | 32 | 0.1 | 128 | 0.001 | 25

Note:  After many iterations of parameter sweeps, we made a couple generalizations that helped us get to our parameters:

* Sentence tokenized embeddings did better with more epochs
* FastText seemed to always perform better with a lower learning rate

## Results

### Result 1 - Classification using Classic Machine Learning Models (TF-IDF)

#### Original Results
##### Performances of CML Classifiers With All Features Using TF-IDF Representations
![CML BagOfWords AllFeatures](https://github.com/chriskabat63/CS598FinalProject/blob/main/images/CML-TFIDF-All.gif?raw=true)

##### Performances of CML Classifiers With Feature Selection Algorithm ExtraTreesClassifier Using TF-IDF Representations
![CML BagOfWords ExtraTreesClassifier](https://github.com/chriskabat63/CS598FinalProject/blob/main/images/CML-TFIDF-Extra.gif?raw=true)

##### Performances of CML Classifiers With Feature Selection Algorithm InfoGain Using TF-IDF Representations
![CML BagOfWords InfoGain](https://github.com/chriskabat63/CS598FinalProject/blob/main/images/CML-TFIDF-InfoGain.gif?raw=true)

##### Performances of CML Classifiers With Feature Selection Algorithm SelectKBest Using TF-IDF Representations
![CML BagOfWords SelectKBest](https://github.com/chriskabat63/CS598FinalProject/blob/main/images/CML-TFIDF-SelectKBest.gif?raw=true)

#### Our Results

##### Performances of CML Classifiers With All Features Using TF-IDF Representations
![CML BagOfWords AllFeatures Results](https://github.com/chriskabat63/CS598FinalProject/blob/main/images/CML-TFIDF-All-Results.png?raw=true)

##### Performances of CML Classifiers With Feature Selection Algorithm ExtraTreesClassifier Using TF-IDF Representations
![CML BagOfWords ExtraTreesClassifier Results](https://github.com/chriskabat63/CS598FinalProject/blob/main/images/CML-TFIDF-Extra-Results.png?raw=true)

##### Performances of CML Classifiers With Feature Selection Algorithm InfoGain Using TF-IDF Representations
![CML BagOfWords InfoGain Results](https://github.com/chriskabat63/CS598FinalProject/blob/main/images/CML-TFIDF-InfoGain-Results.png?raw=true)

##### Performances of CML Classifiers With Feature Selection Algorithm SelectKBest Using TF-IDF Representations
![CML BagOfWords SelectKBest Results](https://github.com/chriskabat63/CS598FinalProject/blob/main/images/CML-TFIDF-SelectKBest-Results.png?raw=true)


#### Notes

**TBD**

### Result 2 - Classification using Deep Learning Models (TF-IDF)

#### Original Results
![DL BagOfWords](https://github.com/chriskabat63/CS598FinalProject/blob/main/images/DL-BagOfWords-ByFeatureSelection.gif?raw=true)

#### Our Results
![DL BagOfWords Results](https://github.com/chriskabat63/CS598FinalProject/blob/main/images/DL-BagOfWords-ByFeatureSelection-Results.png?raw=true)

#### Notes

**TBD**

### Result 3 - Classification using Classical Machine Learning Models (Embeddings)

#### Original Results
![CML Embeddings](https://github.com/chriskabat63/CS598FinalProject/blob/main/images/CML-WE-SWYes.gif?raw=true)

#### Our Results

![CML Embeddings Results](https://github.com/chriskabat63/CS598FinalProject/blob/main/images/CML-WE-SWYes-Results.png?raw=true)

#### Notes

**TBD**

### Result 4 - Classification using Deep Learning Models (Embeddings)

#### Original Results
![DL Embeddings AllFeatures](https://github.com/chriskabat63/CS598FinalProject/blob/main/images/DL-WE-SWYes.gif?raw=true)

#### Our Results
![DL Embeddings Results](https://github.com/chriskabat63/CS598FinalProject/blob/main/images/DL-WE-SWYes-Results.png?raw=true)

#### Notes

**TBD**

### Result 5 - Classification using Ensemble Model

#### Original Results
![Ensemble](https://github.com/chriskabat63/CS598FinalProject/blob/main/images/ensemble.gif?raw=true)

#### Our Results
![Ensemble Results](https://github.com/chriskabat63/CS598FinalProject/blob/main/images/ensemble-Result.png?raw=true)

#### Notes

**TBD**

### Additional Result - Classification using Open AI (Embeddings)

#### Our Results
![DL Embeddings OpenAI Results](https://github.com/chriskabat63/CS598FinalProject/blob/main/images/DL-WE-SWYes-Results.png?raw=true)

#### Notes

The OpenAI embeddings were done using a couple different approaches.  The results shown above used embeddings for each sentence.  It can be seen that the results are very similar to using the USE embeddings (which uses the same sentence tokenizations).  We also ran a single embedding for the entire document.  These results were very close (within ~2%) to the sentence tokenized and required much less processing as the vectors were much smaller (i.e. one vector of 1536 length vs. # sentences *  1536).  We had the greatest success with the ADA v2 embeddings and sentence tokens.  We also tried the Babbage V1 similarity embeddings, but its performance was worse. The Curie and Davinci models were cost prohibitive for this study.

## Computational Results

The classical models were run on a Intel(R) Core(TM) i7-12700KF processor with 32 GB RAM and an NVIDIA GeForce RTX 3080 GPU.

The deep learning models were run on a Intel(R) Core(TM) i7-9750H CPU @ 2.60GHz (6 core/12 threads) with 16 GB of RAM and a NVIDA GeForce GTX 1660 GPU.

The following is a comparison of the CML Models for Bag of Words and Embedding Models:
![Runtime All Models](https://github.com/chriskabat63/CS598FinalProject/blob/main/images/ComputeCML.png?raw=true)

The following is a comparison of the DL Models for Bag of Words and Embedding Models:
![Runtime All Models](https://github.com/chriskabat63/CS598FinalProject/blob/main/images/ComputeDL.png?raw=true)

The following is a comparison of the DL Embedding models using CPU and GPU in both table and graphical representation:
![Runtime GPUCPU Models Table](https://github.com/chriskabat63/CS598FinalProject/blob/main/images/ComputeCPUGPUTable.png?raw=true)
![Runtime GPUCPU Models Graph](https://github.com/chriskabat63/CS598FinalProject/blob/main/images/ComputeCPUGPUGraph.png?raw=true)


## References
Kumar, V., Recupero, D. R., Rbioni, D., & Helaoui, R. (2021). Ensembling Classical Machine Learning and Deep Learning Approaches for Morbidity Identification From Clinical Notes. IEEE Access, 9, 7197-7126. 10.1109/ACCESS.2020.3043221

n2c2 NLP Research Data Sets. (n.d.). DBMI Portal. Retrieved April 12, 2023, from https://portal.dbmi.hms.harvard.edu/
