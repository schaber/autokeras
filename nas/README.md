# Neural Architecture Search

To help the researchers to do experiments on neural architecture search (NAS),
we have implemented several baseline methods using the Auto-Keras framework.
The implementations are easy since only the core part of the search algorithm is needed.
All other parts of NAS (e.g. data structures for storing neural architectures, training of the neural networks)
are done by the Auto-Keras framework.

## Why implement NAS papers in Auto-Keras?

The NAS papers usually evaluate their work with the same dataset (e.g. CIFAR10),
but they are not directly comparable because of the data preparation and training process are different,
the influence of which are significant enough to change the rankings of these NAS methods.

We have implemented some of the NAS methods in the framework.
More state-of-the-art methods are in progress.
There are three advantages of implementing the NAS methods in Auto-Keras.
First, it fairly compares the NAS methods independent from other factors
(e.g. the choice of optimizer, data augmentation).
Second, researchers can easily change the experiment datasets used for NAS.
Many of the currently available NAS implementations couple too much with the dataset used,
which makes it hard to replace the original dataset with a new one.
Third, it saves the effort of finding and running code from different sources.
Different code may have different requirements of dependencies and environments,
which may conflict with each other.

## Baseline methods implemented

We have implemented four NAS baseline methods:
1. random search: we explore the search space via morphing the network architectures randomly, so the actual performance of the generated nerual architecture has no effect on later search.
2. grid search: we manually specified subset of the hyperparameter space to search, i.e., the number of layers and the width of the layers are predefined.
3. greed search: we explore the search space in a greedy way. The "greedy" here means the base architecture for the next iteration of search is chosen from those generated by current iteration, the one that have best performance on the training/validation set in our implementation.
4. bayesian optimization: it's the default search strategy of Auto-Keras currently. refer [arXiv:1806.10282](https://arxiv.org/abs/1806.10282) for more detail. 

## How to run the baseline methods?

Refer to examples/nas/cifar10_tutorial.py for more details.


## How to implement your own search?
To implement your own NAS searcher, you need to implement your own searcher class YOUR_SEARCHER, which is derived 
from base [Searcher](https://github.com/jhfjhfj1/autokeras/blob/master/autokeras/search.py) class. For your 
YOUR_SEARCHER class, you must provide implementation of the abstract method: [generate(self, multiprocessing_queue)](https://github.com/jhfjhfj1/autokeras/blob/d6bea7369186df842dfb8ea3ed779cbd1b8f7c40/autokeras/search.py#L223), 
which is invoked to generate the next neural architecture.

You are welcome to implement your own method for NAS in our framework.
If it works well, we are happy to merge it into our repo.
