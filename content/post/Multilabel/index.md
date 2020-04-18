---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Multi Label Classification using Vowpal Wabbit library: From Why to How"
subtitle: "How to formulate multi label classification task and use Vowpal Wabbit to solve it"
summary: ""
authors: ["admin"]
tags: ["Machine Learning", "Classification"]
categories: ["Technical"]
date: 2020-04-16T21:51:23+05:30
lastmod: 2020-04-16T21:51:23+05:30
featured: false
draft: false
commentable: true
---

#### What is Multi-Label classification?

Think of a recent article/tweet you read and if you were asked to tag it!

Probably you will come up with tags such as technology, politics, fashion, etc. Consider this tweet and try this on your own.

![img](/img/tweet.png)

It can be tagged with self-help, musings, 3 am thoughts! and many others. One can’t say that one is best amongst them. Each one of them is right, you just need a perspective!

One tag may be more appropriate than others, but you can’t have just one tag. We will get back to this afterwards.

Now problems like this arise often in our lives, some more examples are:

- Labelling an image based on its content : (sky, house, grass)
- Genre classification of a movie: (action, adventure, crime)
- Tagging a question asked in Stack Overflow.

#### So what’s the difference between Multi-Class and Multi-Label Classification?

When there are multiple categories but each instance is assigned only one of those categories or classes are mutually exclusive, it’s **multi-class classification**.

When each instance can be assigned multiple categories or classes are related to each other, it’s **multi-label classification.**

#### Standard practices to solve Multi-Label classification problem

Scikit-Learn has provided a separate library [Scikit-Multilabel](http://scikit.ml/) for multi-label classification. I won’t go into details of standard algorithms provided by this library like that would distract from the objective of this blog.

You can have a look at following articles to get handy with this library:

- https://www.analyticsvidhya.com/blog/2017/08/introduction-to-multi-label-classification/
- http://scikit.ml/multilabeldnn.html DL based multi-label classification
- https://towardsdatascience.com/journey-to-the-center-of-multi-label-classification-384c40229bff



#### What is Vowpal Wabbit and why do we need it here?

It’s a library developed by Microsoft Research (previously by Yahoo Inc.) to solve machine learning problems.

> Vowpal Wabbit provides a fast, flexible, online, and active learning solution that empowers you to solve complex interactive machine learning problems.

From what I have experienced, two things set apart this library **speed and online learning.**

> In computer science, **online machine learning** is a method of machine learning in which data becomes available in a sequential order and is used to update our best predictor for future data at each step, as opposed to batch learning techniques which generate the best predictor by learning on the entire training data set at once.



#### Let's dive into our problem

To get a better understanding of Vowpal Wabbit and multi-label classification, let’s unwind the problem of assigning tags to a short textual description.

We will use the *Bibtex* dataset from the [Extreme Classification Library](http://manikvarma.org/downloads/XC/XMLRepository.html) which has 1836 binary features and 159 possible labels for a single text.

<script src="https://gist.github.com/Shivanshmundra/170480784abcc8ff3d4fa98149e6f276.js"></script>

Code for Multi-Label classification using Vowpal Wabbit

For an extensive view, you can head over to the [Github Link](https://github.com/Shivanshmundra/Contextual_Bandits_VowpalWabbit/blob/master/Cost-Sensitive Multilabel Classification .ipynb).

As you might have seen, just iterating over each example once, that too in an online fashion and in blazing speed, model converged to good accuracy.

Let’s understand the algorithm used here(Please read code before going next).



#### Cost-Sensitive Multiclass Classification

Here, instead of just having one correct label (and all others incorrect), you can have different costs for each of the K different labels. And you can also have different “allowable” labels for each example. An identical cost-sensitive training set to that above is:

```
1. 1:0 2:1 3:1 4:1 | a b c
2. 1:1 2:1 3:0 4:1 | b c d
```

The first line means that label 1 has a cost of zero and labels 2, 3 and 4 all have a cost of one. “a, b, c” are binary features associated with example. You can just state features that are present and ignore which are not.

Internally, *csoaa* does something different than you might expect. This problem is reduced to the regression problem. If there are K possible labels, it constructs K *regression* problems, where the input is a (label-based) version of the features and the output is the cost of that label.

And then at test time, the label whose regressor gives the lowest value (predicted cost) is chosen.

------

The objective of this blog was not to find ways to increase accuracy but to introduce this different world of Machine Learning(multi-label classification) and how to efficiently use Vowpal Wabbit to solve it.

There are many modifications/improvements possible in the above solution for example: changing loss function, number of passes over data, optimizing strategy, changing cost for each label, etc.

For more information, you can head over to links below:

- [*http://users.umiacs.umd.edu/~hal/tmp/multiclassVW.html*](http://users.umiacs.umd.edu/~hal/tmp/multiclassVW.html)
- [*https://github.com/VowpalWabbit/vowpal_wabbit/wiki/Cost-Sensitive-One-Against-All-(csoaa)-multi-class-example*](https://github.com/VowpalWabbit/vowpal_wabbit/wiki/Cost-Sensitive-One-Against-All-(csoaa)-multi-class-example)
- [*http://manikvarma.org/downloads/XC/XMLRepository.html*](http://manikvarma.org/downloads/XC/XMLRepository.html)
- [*https://vaillab.blogspot.com/2014/06/mutlti-label-classification-using.html*](https://vaillab.blogspot.com/2014/06/mutlti-label-classification-using.html)

*Any doubts or suggestions feel free to ping me* 😃. *Also, find me on* [*Twitter*](https://twitter.com/MundraShivansh) *and* [*Linkedin*](https://www.linkedin.com/in/shivansh-mundra-300849140/)*. Adios!!*