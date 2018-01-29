## Toxic Comments - Kaggle Challenge

### Introduction

This repo contains code for the [Toxic Comments Kaggle Classification challenge](https://www.kaggle.com/c/jigsaw-toxic-comment-classification-challenge). The goal of the challenge is to classify comments into 6 different potential categories of negative comments.

### Data

The training data for this challenge consists of 159,571 comments from Wikipedia’s talk page edits. Each comment could (and often did) fall under multiple categories.

### Methods

The first step in this project was to process the text into a machine-readable form using Natural Language Processing.

Steps taken in the cleaning process included:
* Replacing meaningless symbols with spaces (such as '@' and next line characters)
* Replacing meaningful symbols with actual words (such as changing '&' to 'and')
* Changing all text to lowercase
* Removing all characters that were not letters
* Lemmatizing the text (i.e., reducing a word to its stem and utilizing contextual information)
* Removing stop words from the text (i.e., commonly used words such as 'the' and 'a')
* Creating tokens and removing any that are not in a known English vocabulary list

After the text was clean, it needed to be converted to a machine readable format using TFIDF. This transforms the text into columns of numbers that indicate a type of normalized frequencies of each token in each comment.

The TFIDF vectorizer and the several options for classifiers were constructed in a pipeline to allow for easier hyper-parameter tuning. The main classifiers tested were those which tend to perform well with imbalanced classes. Tree-based algorithms (such as decision trees & random forests) perform well because their hierarchical structure allows them to take into account multiple classes at each split. K nearest neighbors works well because it is not at all influenced by the total size of the class, only the 'nearest' data points.

### Repository Layout

    ├── README.md               <- The top-level README with a project summary
    │
    ├── models/                 <- Trained and serialized models
    │
    ├── src/                    <- Source code for use in this project
    │   ├── __init__.py         <- Makes the src folder into a Python module
    │   └── main.ipynb          <- Guided notebook for the entire analysis process.
    │
    ├── requirements.txt        <- The requirements file for reproducing the analysis environment;
    │                              generated with `pipreqs .`;
    │                              can be installed using `pip install -r requirements.txt`
    │

### Results

After tuning hyper-parameters using a grid search and cross validation, the final best model with the best hyper-parameters was chosen.

The preliminary cross validation tests on the training data resulted in a weighted f1 score of 58.3. Given the imbalanced classes, a weighted scoring measure was chosen to give importance to both positive and negative comments in each class.

Potential future directions include:
* Try other techniques for working with imbalanced classes, such as downsampling, oversampling, and synthetic sampling (SMOTE)
* Create a custom log loss scoring method for grid-searching with a multi-class classifier (which was the scoring method specified by the Kaggle challenge)
* Create a histogram of word counts in the text to assist in determining what other words should be added to the custom stop words list
* Refactor final code into classes for reproducibility
* Move code to AWS & train model on the entire dataset on the cloud
* Use feature selection techniques to further narrow down the vocabulary used

### Tech Stack

* Python
* Pandas
* Sklearn
* Numpy
* Spacy

### References and Acknowledgements

* Repository layout inspired by the [cookiecutter data science project template](https://drivendata.github.io/cookiecutter-data-science/).
