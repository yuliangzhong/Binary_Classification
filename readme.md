# Binary Classification

## Introduction

The goal of this task is to classify mutations of a human antibody protein into active (1) and inactive (0) based on the provided mutation information. The mutations differ from each other by 4 amino acids in 4 respective sites. The sites or locations of the mutations are fixed. The amino acids at the 4 mutation sites are given as 4-letter combinations (21 in total), where each letter denotes the amino acid at the corresponding mutation site.

* Input data: 'DKWL','FCHN',...
* Input label: 0 or 1

train data and labels are in the *"train.csv"*, and to predict results in *"test.csv"*.

More information, check *"Description.pdf"*

## Solution

### 1. Data Encoding

Data encoding is a very important step for data preprocessing before model training. For this task, we have three data encoding solutions, and guess which one is the best?

* Encode the 4 amino acids as a 4D vector by alphabet: 
'DKWL' ---> [3, 10, 22, 11]
* Encode the 4 amino acids as a 21D vector, one for each: 
'DKWL' ---> [0, 0, 1, 0, 0, 0, 0, 0, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0]
* Encode the 4 amino acids as a 84D vector (**One-hot encoding**): 
'DKWL' --->
[0, 0, **1**, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
0, 0, 0, 0, 0, 0, 0, 0, **1**, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 
0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, **1**, 0, 
0, 0, 0, 0, 0, 0, 0, 0, 0, **1**, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]

The test results show that the third encoding way is the best. The reason is, **when encoding, we should try not to lose information (the second way lose the sequence of amino acids), and try to make feature sparse (for separable classification)**.

### 2. Data Imbalanced

As we can see in the train.csv, we have 112,000 train data in total, but only about 4,000 are labeled as "1". It means that the training dataset is quite imbalanced. We can tackle this problem during implementation.

### 3.  Implementation

SVM and neural network are two popular solutions to classification. We tried them both and let's see the results.

In the code, we implement 3 methods: SVC, MLP and NN(with dropout and batchnorm). Check "solutions.ipynb" for details.

### 4. Results

|Methods|Score |Baseline|Notes|Results|
|:--:|:--:|:--:|:--:|:--:|
|SVC|0.8126|> 0.8526|c=1, rbf| **FAILED**|
|MLP|0.8957|> 0.8526|logistic| **PASS**|
|NN|0.8690|> 0.8526|-----| **PASS**|
