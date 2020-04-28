---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "My Journey to Natural Language Processing"
subtitle: ""
summary: ""
authors: ["admin"]
tags: ["NLP", "PyTorch"]
categories: ["Technical", "Artificial Intelligence"]
date: 2020-04-25T11:59:39+05:30
lastmod: 2020-04-25T11:59:39+05:30
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---

## Natural Language Processing 

I consider the reader to be familiar with normal machine learning terminology and methods. We here are going to deal with Supervised learning mostly. 

Since all machine learning models are mathematical function approximators, we can;t input a sentence to a mathematical model!

There is nothing like `f('I am here to learn NLP')`, one need to convert from our language to machine language so that it becomes something like `f([1, 0, 1, 2, 5 ..])`, since this is the method computer is most familiar with. So first jumping to this conversion:



### Conversion of text to mathematical representation

#### 1. Basic Approach of making dictionary

Here you just create a dictionary or set of all available words present in data and represent each word/sentence with one hot vector. For example : Let's say we have 8 words in our dictionary and sentence `I like banana` is to be encoded, it would be something like `[1,0,0,0,1,0,0,1]` where index representing `I, like and Banana`. In this case, length of this vector would be fixed and equal to vocabulary of data.

In this case, there is no sense of context here, `like` can be used in different context yet same representation.  But duh! It's the first method and supposed to be this dumb!

#### 2. TF-IDF Representation

Full form is : **Term Frequency-Inverse Document Frequency** . The full form mentioned is self explanatory still we would want to get a feel. So here it is: 

Term-Frequency representation means number of times a word is occurring and represent in one hot vector by it's frequency for ex `[1,2,0,0,3]`. Now in this case, let's say there is a common word `the` which is occurring in most of corpus(another name for sentence!) but adds no specific meaning to understanding. So we take TF representation and multiply it with IDF which is $log(N/nw)$ where N is total number of document/corpus  and nw is number of corpus which contain that word. Smart thinking!

We won't use this in our supervised learning paradigm, we would just go with one hot vector and prepare embedding for our model.





### Terminologies

- Corpus(singular- Corpura) : A sentence or document in general consisting of words. 
- Tokenization: Splitting a corpus based on white spaces(in general) in between(for English specifically). 
  - Say a sentence `I want to learn Tokenization :-)` is to be tokenized.
  - Tokenization would be `['I', 'want', 'to', 'learn', 'Tokenization', ':-)']` 
  - There are several libraries which use context and tokenize the corpus.
- N-gram tokens: Taking consecutive `n` tokens from tokenized representation in contiguous manner.
- POS Tagging: Categorising tokens to parts of speech.
- Dependency Parsing: Extracting relationship/dependency between different tokens in sentence.



### Workflow of NLP Pipeline

In every NLP data, there are three main components: 

**The Vocabulary:** We want a bijection mapping where we map tokens to mathematical integers. We create a dictionary mapping tokens to indexes. This would also contain index to token mapping.  

**The Vectorizer**: This method produces vectors from text/corpus using vocabulary above.

**The Dataloader**: Traditional data science batchloader which yield data points in rolling fashion.

 