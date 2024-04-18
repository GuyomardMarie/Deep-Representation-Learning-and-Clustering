# Evaluate the Representation Learning task on Clustering

# Functions

We provide functions to compute and evaluate Clustering. 2 methods are implemented; K-means and Gaussian Mixture Models (GMM).

The different functionalities are the following:

1. Function to fit clusters: *fit_cluster*
    This function handles 2 types of clustering: K-means and GMM. It necessitates as parameter the number of cluster (resp. guassian mixtures for GMM).

2. Function to predict clusters: *predict_cluster*
    This function applies the model on a sample to attribute clusters.

3. Functions to evaluate the clusters on the training sample and validation set: *evaluate_cluster_train* and *evaluate_cluster_validation*
    These functions compute the following metrics: 
    - Silhouette score
    - Intra-cluster inertia: measures the sum of squares of distances between each data point and its assigned cluster centroid.
    - Extra-cluster inertia: measures the total dispersion of data points relative to their centroids.
    - Davies-Bouldin index: measures the average similarity between each cluster and its most similar clusters. A lower value indicates better separation between clusters.

4. Function to optimize the hyperparameter: *gridsearch_cluster_hyperparametres*
    This function aims at selectinig the optimal number of clusters for K-means and Gaussian Mixtures for GMMs.

5. Function to compute a Cross-Validation: *train_cluster_CV*
    This function:
    - Split the sample into a training set (80%) and a test one (20%)
    - Train the clustering task on the training set (function fit_cluster)
    - The model is then applied to both training and validation sets (function predict_cluster)
    - The different metrics are computed on both samples (functions evaluate_cluster_train and evaluate_cluster_validation)
    - 2 Dataframes are returned (one on the training and on the validation test) containing for each fold the different metrics

6. Function to visualize the clusters through PCA or t-SNE dimension reduction techniques: *PCA_caracteristic*
    
    This function is developed for maximum 5 clusters. It takes as input a dataframe containing the different attributes of the samples (categorical variable, for example Chemiotherapy Y/N or type of Chemiotherapy = {adjuvant, neoadjuvant, both}). For each attribute, a plot is displayed emphasizing the distribution of the different values of attributes regarding the cluster the sample belong to.
    
# Main

In this notebook, all the steps aiming at evaluating a pre-trained Representation Learning methods are detailed:

1. Load the patient representation, this will be the input data for the clustering task
2. Cross-Validation to evaluate the quality of the clustering task
    - Gridsearch of the optimal number of clusters
    - Training and Validation of the model with the optimal number of clusters
3. Validation of the clustering reliability through chi-squared test
    - A dataframe of attributes (categorical variable) has to be loaded
    - The statistical test is performed on randomly generated 5 submsamples
    - The statistical test is performed regarding the patients' clinical reality
    - A small p-value (<0.05) indicates that the hypothesis of independance between the cluster label and the attribute is not accepted. Thus the clustering task is discriminant regarding this clinical attribute.
  
  4. Validation of the clustering task through PCA and t-SNE reduction dimension techniques
     - The dimension reduction technique (PCA or t-SNE) is performed to the whole sample
     - The PCA (resp. t-SNE) visualizations are displayed regarding the different clinical attributes; for each value taken by the considerated attribute, a plot is displayed emphasizing the specific samples with this value regarding the cluster they belong to.
