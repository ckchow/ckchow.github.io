---
layout: post
title: "Experiments in Deep Learning"
categories: machine-learning
---

The problem is that you have a bunch of experiments that you have done, but
you were lazy when you did them and didn't capture all of the important context
for each experiment when you ran it. That's bad! It is very important to have a
clear methodology when you are doing empirical stuff. Lots of tutorials just
teach you how to use a deep learning framework for doing something, not how to
use the scientific method to get clear and consistent results.

With that in mind, our quest is to find out what combination of
cool deep learning tricks we can combine to make a classifier work best at
classifying a particular dataset. This is a bit of a weird experiment because
we don't have a concrete hypothesis at this point, more of an intuition that
there is a combination of parameters that will allow us to classify a given
dataset well (which is a reasonable assumption), and a bunch of knowledge about
deep learning tricks.

What we are doing then is multiple iterations of hypothesis refinement to
design the hypothesis with the highest accuracy, using our intuition and knowledge about deep learning to
guide us to the best spot in configuration space.

A brief aside is that automated methods using gaussian processes might be even
better than people at figuring out these intuitive tricks but that's a
discussion for another day.

Anyway, the first hypothesis would be something like:
> A fine-tuned imagenet model will classify this dataset well

We run our experiment (fine-tune the model, evaluate the model on our val set)
and collect the result (accuracy, F1, etc...). This result is probably not good
enough for us. So now we have to refine our hypothesis. Before we do that, let's
see what kind of variables on our hypothesis that we can mess with. This is an
important step that you should probably do after every experimental run.

## Training variables
- learning settings
  - batch size
  - learning rate (per layer, potentially)
  - weight decay
  - regularizations
- augmentation strategy
- network structure (probably the name of the net that is loaded)
- dataset (or hash of the dataset, since the dataset is probably large)

## Performance metrics
- Accuracy
- Loss (logloss in this case)

## Just for fun
- date of run
- runtime
- other notes

Some of this data can be subsumed into the "other notes" category, but that
makes sorting runs by condition hard, and also makes it likely that you will
miss combinations in the configuration space.

All these variables systematically capture your intuition about the problem and
your hypothesis, and allow you to efficiently explore the configuration space.
Eventually you can use these notes to convince someone that you know what you
are doing.

The next step is to make another, better hypothesis. Like:
>  fine-tuning inception-resnet-v2 with an augmentation strategy that makes use of
>  color distortion, rotations, and noise will classify this dataset better than
>  my previous attempt
