### Introduction

This is deep learning code for running experiments the Paradigm Cell Filling Problem (PCFP). The code is meant for running the experiments in the paper

Miikka Silfverberg and Mans Hulden. 2018. *An Encoder-Decoder Approach to the Paradigm Cell Filling Problem*. EMNLP.

In PCFP, you are given a number of partial inflection tables. For example,

```
walk         V;INF
             PRES;3SG
walk         PRES;NON3SG
             PAST
             PCPLE;PAST
walking      PCPLE;PRES
```

and the objective is to fill in the missing forms in all the tables

```
walk         V;INF
walks        PRES;3SG
walk         PRES;NON3SG
walked       PAST
walked       PCPLE;PAST
walking      PCPLE;PRES
```

We experiment with three settings.

* n > 1 word forms are given in each paradigm.  
* Exactly n = 1 word form is given in each paradigm.  
* The 10,000 most frequent forms (according to Wikipedia frequency) are given and the remaining forms in their inflection tables are unknown.

Note, that in the last setting, inflection tables may contain varying
numbers of forms. For some lexemes like the English "be", many forms
like "is" and "was" will be among the top 10,000 forms. For others,
perhaps only one of the forms is frequent and the rest are infrequent.

Additionally, we compare against the model presented in 

Robert Malouf. 2017. _Abstractive morphological learning with a recurrent neural network_. Morphology. 

### Requirements

You need Python 3 and DyNet. This code has been tested on DyNet version 2.0

### Training and Testing Models

You should use 
   * `train_n_gt_1.py` and `test_n_gt_1.py` for training and testing models when n > 1 models are given in each table.
   * `train_n_eq_1.py` and `test_n_eq_1.py` for training and testing models when n = 1 models are given in each table.
   * `train_top_10000.py` and `test_n_gt_1.py` for training and testing models when the top 10,000 models are given in each table.
   * `train_malouf.py` and `test_malouf.py` for training and testing Malouf (2016) models.
   
The `train_XYZ.py` scripts are used for training models. The usage is the following

```
python3 train_XYZ.py input_data_file output_model_file
```

The `test_XYZ.py` scripts are used for testing models. The usage is the following

```
python3 test_XYZ.py input_data_file model_file > output_data_file
``` 

### Voting

Given 10 output files `somedata.output.1`, ..., `somedata.output.10`, you can perform voting by

```
python3 vote.py somedata.output 10 > somedata.output.vote
```
