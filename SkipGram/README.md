# Skip-Gram Representation

## References 

Distributed Representations of Words and Phrases and their Compositionality, Tomas Mikolov et al (2013)

Learning Low-Dimensional Representations of Medical Concepts, Youngduck Choi (2016)

Medical Concept Representation Learning from Electronic Health Records and its Application on Heart Failure Prediction, Edward Choi (2016)

Patient Embeddings From Diagnosis Codes for Health Care Prediction Tasks: Pat2Vec Machine Learning Framework, Steiger (2023)

Doctor AI: Predicting Clinical Events via Recurrent Neural Networks, Edward Choi (2016)


## Python environment 
- Python 3.10
- Required Packages: pytorch, pandas and scikit-learn


## Functions

We provide all the needed functionnalities to compute patient representations using Skip-Gram algorithm:
- A function to prepare the data: *Word2VecDataset*

  This function creates word pairs. For each time sequence (i.e., each patient):
    - It iterates over each code to find its neighbors. If window_size = 5, then it takes 5 neighbors, ie. the 5 codes following the target one.
    - It generates 'negative samples': num_negative_samples indicates the number of negative samples.
  
  This function returns a list of tuples (target_word, context_word, label). The label indicates if it is a positive sample (a true neighbor) or a negative one (a false one).
  
              Example:
              
              If window_size = 5 and num_negative_samples = 3, then one obtains:
              [[451, 525, 1],
               [451, 817, 1],
               [451, 818, 1],
               [451, 579, 1],
               [451, 579, 1],
               [451, 530, 0],
               [451, 530, 0],
               [451, 659, 0],...]
              with 525, 817, 818, 579 the true neighbors (label=1) of the target code 451 and 530, 659 the false ones (label=0)
              
- A class for the model: *Word2Vec*
  
    This class is responsible for constructing the Word2Vec model. It requires two parameters:
    - vocab_size (int): the number of unique words (i.e., codes)
    - embedding_dim (int): the size of the embedding space
    
    The forward function takes two tensors as input:
    - target: the word on which Skip-Gram is applied
    - context: the context word
    
    It returns the matrix multiplication between the representation of the target word and that of its neighbor.
    

- A Gridsearch of the hyperparameters function: *Train_Word2Vec*

  This function optimizes the model hyperparameters. The hyperparameters tested are:
    - window_size: the size of the window (i.e., the number of considered neighbors)
    - emb_size: the size of the embedding
    - num_negative_samples: the number of generated negative samples
    - batch_size: the number of sequences per batch
  
  The different steps of the function are fully discribed in the notebook.

- A training function: *Train_Word2Vec*
This function is used to train the model. It takes 5 parameters:
  - embedding_dim (int): the dimension of the embedding
  - vocab (dict): unique words in the corpus
  - nb_epoch (int): the number of iterations
  - learning_rate (float): the gradient step size
  - batch_size (int): the size of batches

Further details are provided in the notebook.


## Main

In this notebook, the various steps for training Skip-Gram representations are provided:

1. Preparation of the data
    - The data are transformed into a list of codes sequences per patient
        Example:
        If the first patient has 3 visits (Code1, Code2, Code3) and the second one 2 visits (Code4, Code2), the shape of the data will be 
        [[Code1, Code2, Code3], [Code4, Code2]]
    - A dictionnary of all unique medical codes is required: {'code' (str), id (int), ...}


2. Gridsearch of the hyperparameters
    - The parameters to be tested must be specified in a list.
    - Training parameters to set: number of epochs, learning rate.

3. Training Step
    - Data Preparation
    - The sample is split into a train set (80%) and a validation set (20%).
    - Generate DataLoader
    - Training parameters to specify: number of epochs, learning rate, and batch size.

4. Evaluation: Compare the losses obtained on the train set and the validation set to prevent overfitting.

5. Obtain the resulting patient representations
     - Get the code representations by applying the model to all the unique codes
     - Get the patient representations by summing the code representations appearing in a patient sequence



