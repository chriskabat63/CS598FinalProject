# Reproducibility Project for CS598 DL4H in Spring 2023

Matthew Lopes and Chris Kabat

{mlopes2, cjkabat2}@illinois.edu

Group ID: 59

Paper ID: 156

Presentation link: TBD


# Introduction

The paper we have chosen for the reproducibility project is:
Ensembling Classical Machine Learning and Deep Learning Approaches for Morbidity Identification from Clinical Notes (Kumar, V., Recupero, D. R., Rbioni, D., & Helaoui, R., 2021, 7197-7126)

The main goal of the paper is to extract co-morbidity recognition from clinical notes.  The idea was to use a combination of classical (CML) and deep learning methods(DML) to determine the best approach for classifying these notes in one or more of 16 morbidity conditions.  These models used a combination of NLP techniques including embeddings and bag of words implementations to provide input into the models.  It also measured the effect of including and removing stop words.  Lastly, it used ensemble techniques to tie together a number of the classical and deep learning models to provide the most accurate results.

The goal of our reproducibility study is to confirm the claims made in the paper as well as show how some additional techniques can be used to improve results.

## Methodology

## Notebooks

[Data Preperation](https://github.com/chriskabat63/CS598FinalProject/blob/main/Project%20Workbook%20Data%20Preparation%20-%20156.ipynb)


[Classical ML Models](https://github.com/chriskabat63/CS598FinalProject/blob/main/Project%20Workbook%20Classical%20ML%20Models%20-%20156.ipynb)


[Create Embeddings](https://github.com/chriskabat63/CS598FinalProject/blob/main/Project%20Workbook%20Create%20Embeddings%20-%20156.ipynb)


[Deep Learning Models](https://github.com/chriskabat63/CS598FinalProject/blob/main/Project%20Workbook%20Deep%20Learning%20ML%20Models%20-%20156.ipynb)


[Ensemble Models](https://github.com/chriskabat63/CS598FinalProject/blob/main/Project%20Workbook%20Ensemble%20Models%20-%20156.ipynb)



## Parameter Tuning

## Results

### Result 1 - Classification using Classic Machine Learning Models (TF-IDF)

#### Original Results
#### Performances of CML Classifiers With All Features Using TF-IDF Representations
![DL BagOfWords AllFeatures Averaged](https://github.com/chriskabat63/CS598FinalProject/blob/main/images/CML-TFIDF-All.gif?raw=true)

#### Performances of CML Classifiers With Feature Selection Algorithm ExtraTreesClassifier Using TF-IDF Representations
![DL BagOfWords AllFeatures Averaged](https://github.com/chriskabat63/CS598FinalProject/blob/main/images/CML-TFIDF-Extra.gif?raw=true)

#### Performances of CML Classifiers With Feature Selection Algorithm InfoGain Using TF-IDF Representations
![DL BagOfWords AllFeatures Averaged](https://github.com/chriskabat63/CS598FinalProject/blob/main/images/CML-TFIDF-InfoGain.gif?raw=true)

#### Performances of CML Classifiers With Feature Selection Algorithm SelectKBest Using TF-IDF Representations
![DL BagOfWords AllFeatures Averaged](https://github.com/chriskabat63/CS598FinalProject/blob/main/images/CML-TFIDF-SelectKBest.gif?raw=true)

#### Our Results

#### Notes

### Result 2 - Classification using Deep Learning Models (TF-IDF)

#### Original Results
![DL BagOfWords AllFeatures Averaged](https://github.com/chriskabat63/CS598FinalProject/blob/main/images/CML-WE-SWYes.gif?raw=true)

#### Our Results

#### Notes

### Result 3 - Classification using Classical Machine Learning Models (Embeddings)

#### Original Results
![DL BagOfWords AllFeatures Averaged](https://github.com/chriskabat63/CS598FinalProject/blob/main/images/DL-BagOfWords-ByFeatureSelection.gif?raw=true)

#### Our Results

#### Notes

### Result 4 - Classification using Deep Learning Models (Embeddings)

#### Original Results
![DL BagOfWords AllFeatures Averaged](https://github.com/chriskabat63/CS598FinalProject/blob/main/images/DL-WE-SWYes.gif?raw=true)

#### Our Results

#### Notes

### Result 5 - Classification using Ensemble Model

#### Original Results
![DL BagOfWords AllFeatures Averaged](https://github.com/chriskabat63/CS598FinalProject/blob/main/images/ensemble.gif?raw=true)

#### Our Results

#### Notes

### Additional Result - Classification using Open AI (Embeddings)

#### Our Results

#### Notes


## References
Kumar, V., Recupero, D. R., Rbioni, D., & Helaoui, R. (2021). Ensembling Classical Machine Learning and Deep Learning Approaches for Morbidity Identification From Clinical Notes. IEEE Access, 9, 7197-7126. 10.1109/ACCESS.2020.3043221
