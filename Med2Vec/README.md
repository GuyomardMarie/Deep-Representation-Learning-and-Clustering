# Med2Vec

## References

Multi-layer Representation Learning for Medical Concepts, E. Choi (2016)

RETAIN: Interpretable Predictive Model in Healthcare using Reverse Time Attention Mechanism, E. Choi (2016)

Doctor AI: Predicting Clinical Events via Recurrent Neural Networks; E. Choi (2016)

Github with the authors codes

https://github.com/mp2893/med2vec


## Python environnement

- Python 2.7
- Required Packages: Theano, Pickle, Scikit-learn and Scipy


## Complementary Functions

1. En evaluation function: Evaluate_Med2Vec

   This function ables to compute the loss of a trained model on a new sample (different than the one used to fit the model)

3. A Training Function: Train_Med2Vec
    
  This function ables to train and evaluate the model on a validation sample to prevent overfitting:
  
  - Split the sample into a train set (80%) and a validation one (20%)
  - Train the Med2Vec architecture on the training sample
  - Evaluate the model on both training and validation samples by computing the losses
  - Returns the losses on the training and test sets

3. Gridsearch of hyperparameters

    This function aims at optimizing the following hyperparameters composing Med2Vec model:
   
    - embDimSize: dimension of the intermediate latent space
    - hiddenDimSize: dimension of the latent space 
    - window_size: size of the context window 

    All set of hyperparameters to be tested given as input are used to train the model on a training set (80% of the sample). 

    The optimal set of hyperparameters is the one minimizing the loss function on a validation sample (20% of the sample).


## Main

In this notebook, the various steps for training Med2Vec representations are provided:

1. Data Preparation
   
  The format of the data required by the original package is a pickled list, such as each sample is separated by a token [-1].

      Example:
      - Sample 1 - 2 visits: [1,2,3], [4,5,6,7]
      - Sample 2 - 3 visits: [2,4], [8,3,1], [3]
      - Final input: [[1,2,3], [4,5,6,7], [-1], [2,4], [8,3,1], [3]]

  This list has to be pickled.

  2. Gridsearch of the hyperparameters

    - The parameters to be tested must be specified in a list.
    - Training parameters to set: number of epochs, learning rate, and batch size.
    
4. Training and Validation Steps
   
  - The sample is split into a train set (80%) and a validation set (20%).
  - Evaluation of the loss on the validation sample to prevent overfitting
  - Training parameters to specify: number of epochs, learning rate, and batch size.

4. Obtain the resulting patient representations by applying the model to the entire sample.

## Remark on the File of parameters

For each provided functions, a File (dict) is required to specify the parameters, as in the initial package.
        File : dict
        
        Dictionnary with the following keys :
        
        - 'seqFile' (str) : The path to the Pickled file containing visit information of patients
        
        - 'labelFile' (str) : The path to the Pickled file containing grouped visit information of patients
        
        - 'outFile' (str) : The path to the output models
        
        - 'demoFile' (str) : The path to the Pickled file containing demographic information of patients
        
        - 'numXcodes' (int) : The number of unique input medical codes
        
        - 'numYcodes' (int) : The number of unique output medical codes (the number of unique grouped codes)
        
        - 'demoSize' (int) : The size of the demographic information vector
        
        - 'embDimSize' (int) : The size of the code representation
        
        - 'hiddenDimSize' (int) : The size of the visit representation
        
        - 'windowSize' (int) : The size of the visit context window (range: 1,2,3,4,5)
        
        - 'batchSize' (int) : The size of the demographic information vector
        
        - 'maxEpochs' (int) : The number of training epochs
        
        - 'logEps' (float) : The learning rate
        
        - 'L2_reg' (float) : L2 regularization for the code representation matrix W_c


