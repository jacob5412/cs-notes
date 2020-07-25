# What is the Difference Between Test and Validation Datasets?

* Training set: A set of examples used for learning, that is to fit the parameters of the classifier.
* Validation (or hold out) set: A set of examples used to tune the parameters of a classifier, for example to choose the number of hidden units in a neural network. The evaluation becomes more biased as skill on the validation dataset is incorporated into the model configuration.
* Test set: A set of examples used only to assess the performance of a fully-specified classifier. Provides an unbiased evaluation of a final model fit on the training dataset. The error on the test set provides an unbiased estimate of the generalization error (assuming that the test set is representative of the population, etc.).

### Pseudocode

```python
# split data
data = ...
train, validation, test = split(data)

# tune model hyperparameters
parameters = ...
for params in parameters:
	model = fit(train, params)
	skill = evaluate(model, validation)

# evaluate final model for comparison with other models
model = fit(best_params)
skill = evaluate(model, test)
```

## Validation Dataset Is Not Enough

* use k-fold cross-validation to tune model hyperparameters instead of a separate validation dataset.
* recommend the bootstrap method in the case of comparing model performance because of the low variance in the performance estimate.

### Pseudocode:

```python
# split data
data = ...
train, test = split(data)

# tune model hyperparameters
parameters = ...
k = ...
for params in parameters:
	skills = list()
	for i in k:
		fold_train, fold_val = cv_split(i, k, train)
		model = fit(fold_train, params)
		skill_estimate = evaluate(model, fold_val)
		skills.append(skill_estimate)
	skill = summarize(skills)

# evaluate final model for comparison with other models
model = fit(train)
skill = evaluate(model, test)
```

## References

1. [Machine Learning Mastery - What is the Difference Between Test and Validation Datasets?](https://machinelearningmastery.com/difference-test-validation-datasets/)
2. [Brian Ripley, page 354, Pattern Recognition and Neural Networks, 1996](https://www.amazon.com/dp/0521717701?tag=inspiredalgor-20)