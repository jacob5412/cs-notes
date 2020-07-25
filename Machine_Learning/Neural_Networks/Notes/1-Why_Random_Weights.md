# Why Initialize a Neural Network with Random Weights?

## Deterministic and Non-Deterministic Algorithms

### Deterministic

* E.g: each time a sorting algorithm is given the same list, it will execute in exactly the same way
* will make the same moves at each step of the procedure
* they can make guarantees about best, worst, and average running time
* but not suitable for all problems

### Non-Deterministic

* use elements of randomness when making decisions during the execution of the algorithm
* a different order of steps will be followed when the same algorithm is rerun on the same data
* rapidly speed up process of getting solution
* but solution will be a good approximate
* Required as a deterministic algorithm cannot be used to solve them efficiently

## Stochastic Search Algorithms

* not entirely random
* random within a bound
* E.g. genetic algorithm, simulated annealing, and stochastic gradient descent
* search process is incremental from a starting point in the space of possible solutions toward some good enough solution

### Use of Randomness

1. during initialization
2. during the progression of the search

* We know nothing about the structure of the search space
* Therefore, to remove bias from the search process, we start from a randomly chosen position
* As the search process unfolds, there is a risk that we are stuck in an unfavorable area of the search space - local optima
* Using randomness during the search process gives some likelihood of getting unstuck and finding a better final candidate solution

## Random Initialization in Neural Networks

* weights of ANN must be initialized to small random numbers
* this is an expectation of the stochastic optimization algorithm used to train the model, called **stochastic gradient descent**
* The progression of the search or learning of a neural network is referred to as **convergence**
* The discovering of a sub-optimal solution or local optima is referred to as **premature convergence**
* **multiple restart or multiple-restart search**: repeat the search process multiple times and report the average performance of the model over those repeats
* Gives the configuration the best chance to search the space from multiple different sets of initial conditions

### Why Not Set Weights to Zero?

* the equations of the learning algorithm would fail to make any changes to the network weights, and the model will be stuck
* nodes that are side-by-side in a hidden layer connected to the same inputs must have different weights for the learning algorithm to update the weights

### When to Initialize to the Same Weights?

* This would not be helpful when evaluating network configurations
* Useful in the case where a model is being used in a production environment

## Initialization Methods

* **Zeros**: Initializer that generates tensors initialized to 0.
* **Ones**: Initializer that generates tensors initialized to 1.
* **Constant**: Initializer that generates tensors initialized to a constant value.
* **RandomNormal**: Initializer that generates tensors with a normal distribution.
* **RandomUniform**: Initializer that generates tensors with a uniform distribution.
* **TruncatedNormal**: Initializer that generates a truncated normal distribution.
* **VarianceScaling**: Initializer capable of adapting its scale to the shape of weights.
* **Orthogonal**: Initializer that generates a random orthogonal matrix.
* **Identity**: Initializer that generates the identity matrix.
* **lecun_uniform**: LeCun uniform initializer.
* **glorot_normal**: Glorot normal initializer, also called Xavier normal initializer.
* **glorot_uniform**: Glorot uniform initializer, also called Xavier uniform initializer.
* **he_normal**: He normal initializer.
* **lecun_normal**: LeCun normal initializer.
* **he_uniform**: He uniform variance scaling initializer.

## References

1. [Machine Learning Mastery](https://machinelearningmastery.com/why-initialize-a-neural-network-with-random-weights/)