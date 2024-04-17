# Deep Patient Representation


## References

Miotto, R., Li, L., Kidd, B. A. et Dudley, J. T. (2016). Deep patient: an unsupervised representation to predict the future of patients from the electronic health records. Scientific reports, 6(1):1–10

Github with the authors codes
https://github.com/riccardomiotto/deep_patient


## Python environnement

- Python 2.7
- Required Packages : Theano, Scikit-learn, Pandas and Scipy


## Functions

We provide 2 complementary functionalities from the existing package

1. A Gridsearch function: gridsearch_sda

    This function aims at optimizing the following hyperparameters composing Deep Patient architecture:
    - nhidden: dimension of the latent space
    - nlayer: number of Autoencoder layers
    - corrup_lvl: data corruption level

    All set of hyperparameters to be tested given as input are used to train the model on a training set (80% of the sample). 

    The optimal set of hyperparameters is the one minimizing the loss function on a validation sample (20% of the sample).



2. An Evaluation function : evaluate_sda

    This function compute the cost of the model on both training and validation set.

## Main

In this notebook, the various steps for training Deep Patient representations are provided:

1. Data Preparation
  - Medical codes must be factorized: each medical code in string format is assigned an integer.
  - Padding is necessary to ensure all patients have sequences of visits of the same length (see authors' GitHub).
  - Finally, the data needs to be formatted into a matrix of shape (number of samples x max length of visit sequences).


2. Gridsearch Step
  - The parameters to be tested must be specified in a list.
  - Training parameters to set: number of epochs, learning rate, and batch size.


3. Training Step
  - The sample is split into a train set (80%) and a validation set (20%).
  - Training parameters to specify: number of epochs, learning rate, and batch size.

4. Evaluation: Compare the losses obtained on the train set and the validation set to prevent overfitting.

5. Obtain the resulting patient representations by applying the model to the entire sample.
