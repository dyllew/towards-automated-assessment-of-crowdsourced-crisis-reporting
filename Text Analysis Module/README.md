# **Text Analysis Module**

### **URL Text Analysis Module Python Package**
The URL Text Module Python package is used throughout the notebooks we developed in our text analysis and is open-sourced under the Apache 2.0 License. This package is available on PyPI [here](https://pypi.org/project/url-text-module/). The package repository can be found [here](https://gitlab.com/react76/url-text-module). We note that we used version 0.6.1 of the package in this work.

### **Text Analysis Methodology -- Exploratory Data Analysis (EDA), Classification, Clustering, and Evaluation in Fukuchiyama City, Japan**
Below we list the order & purpose of various Jupyter notebooks used for conducting our analysis on crisis text data from Fukuchiyama, Japan (we sometimes denote Fukuchiyama as FC). We investigated real crisis text data from reports by on-the-ground firefighters in Fukuchiyama during past flood events. These reports are in Japanese (JA). Our text analysis methodology involved cleaning the original data, performing exploratory data analysis, conducting classification experiments using labels provided by our partners in Fukuchiyama to enable informative & accurate predictions during a crisis event, and lastly we performed clustering experiments & analysis to assist in informing future labels of the text data in future work.

**IMPORTANT NOTES:** 
* We are unable to open-source the text data we were provided by our partners in Fukuchiyama. Furthermore, any auxiliary outputs which show the original text inputs also cannot be open-sourced, however, the utilities we developed for conducting our analysis and experiments are reusable and are open-sourced for use in future work. We aim to demonstrate these developed utilities in the notebooks described below.
* All of these notebooks were run on a Google Colab machine

### **Cleaning, Exploratory Data Analysis (EDA), Preprocessing and Featurization of the Text Data**
---
1. **Refactoring the original dataset CSV & cleaning the corresponding pandas DataFrame:**
* Alters pandas DataFrame containing the original Fukuchiyama text data by renaming columns of the dataframe to their corresponding name in the URL text module Python package essentially to enable compatibility with the utilities in the URL text module.
* Cleans the dataframe by removing any rows with all blank entries, i.e. where the value of each column is n/a for a row, and any row which is missing the input text string.
- Directory: [./Cleaning, EDA, and Preprocessing]()
- Notebook: [./Cleaning, EDA, and Preprocessing/Clean_FC_txt_data.ipynb]()
2. **Exploratory Data Analysis:**
* Using the cleaned dataframe from the step above, performs EDA by investigating the frequencies of unique categories given to the text reports by personnel at the fire department headquarters (FDHQ), the distribution of the character counts of the Firefighter text reports and comparing it against a text dataset from RiskMap during Typhoon Hagibis in Tokyo, Japan. 
* Variations of "Yes" & "No" labels were provided by personnel at the FDHQ for classifying whether or not a text report was indicative of Human Risk. This notebook corrects the variations to be "Yes" & "No" labels and plots the final distribution of the labels across the data set to see the extent of class imbalance for the task.

- Directory: [./Cleaning, EDA, and Preprocessing]()
- Notebook: [./Cleaning, EDA, and Preprocessing/FC_txt_data_EDA.ipynb]()
- Misc: The plots created during the EDA can be found [here]().

3. **Preprocessing & Featurization of the Raw Input Text:**
* Using the cleaned firefigheter report dataset from the above steps, applies a preprocessing pipeline which first tokenizes the text strings into word tokens using the pretrained tokenizer, Fugashi, then uses an open-source set of Japanese stopwords to remove stopword tokens, and then converts tokens into their lemma (or dictionary) form. 
* Alternatively, uses a pretrained BERT model trained for Masked Language Modeling objective on the Japanese version of Wikipedia to extract contextualized embeddings (this process is also known as CLS Pooling) of the input firefighter text reports with minimal preprocessing. The proprocessed and tokenized documents as well as the BERT embeddings are then used in the classification and clustering experiments in the notebooks below.

- Directory: [./Cleaning, EDA, and Preprocessing]()
- Notebook: [./Cleaning, EDA, and Preprocessing/FC_txt_preprocessing.ipynb]()

### **Classification of Fukuchiyama Crisis Text Data**
---
4. **Classification of the FC Firefighter Text Reports for the binary Human Risk Task**

**Data & Model Preparation For Human Risk Classification Experiments**
* Splits the data (the raw input text, tokenized documents, and BERT embeddings discussed above) labeled for the binary (Yes/No) Human Risk task into Train and Test sets into percentages of 80%/20, respectively, of the original dataset. We note that this splitting is stratified meaning that the proportion of the yes/no labels in the original dataset is preserved in the training and test sets.
* Defines the hyperparameter + featurization grids and the type of normalization to apply to the featurization to algorithm for several classification algorithms including: Logistic Regression (LR), Random Forest (RF), Decision Tree (DT), Multinomial Naive Bayes (MB), K-Nearest Neighbors (KNN), and Support Vector Machine (SVM)

**Nested Cross Validation (Nested CV) for Algorithm Selection on Training Set**
* Performs 5 by 5 Nested CV (with Grid Search) for the algorithm and corresponding hyperparameter + featurization grids (for algorithm selection) mentioned above and plots the mean and standard deviation of the F2 score for each on the outer cross validation test folds. This procedure is done using the train dataset mentioned above. We note that stratified cross validation is used in which the proportions of the Yes/No labels in the training set are preserved in the train/test folds of the Nested CV inner & outer cross validation procedures. Saves defined grids for each algorithm and related intermediate results, final results, and metadata from the Nested CV procedure in the [Nested CV]() directory.

**Stratified Cross Validation on Support Vector Machine (SVM) and its corresponding grid on Training Set**
* SVM (& its corresponding hyperparameter + featurization grid) gives the highest mean F2 score (82.0%) and lowest standard deviation (4.22%), so 5-fold cross validation validation (with Grid Search) is performed using the SVM algorithm & its associated hyperparameter and featurization grid to find the best hyperparameter and featurization combination which has the highest mean F2 score across the test folds. Saves final and intermediate results and metadata from the cross validation procedure in the [SVM_CV_TUNING]() directory.

**Final SVM Model Evaluation on Test Set**
* Using the SVM model fitted on the entire training set with the hyperparameter + featurization combination which had the highest mean F2 score from the CV procedure, the model is evaluted on the test set in which the the Area Under the Precision Recall (AUCPR: 0.919) and the F2 score (F2: 0.928) are computed for the fitted SVM model. These scores are compared to a variety of baseline "dummy" classification strategies including the classifier which always predicts "Human Risk" (AUCPR: 0.566/ F2: 0.434)
* The precision-recall curve is plotted for the fitted SVM model on the test set using its decision score function. Additionally, the confusion matrix of the SVM model on the test set is plotted as well as the per-class precision, recall, and F1 scores.

**Model Preparation for Future Inferencing**
* The SVM model is fitted to the entire dataset (both train + test sets) for future inferencing for the binary Human Risk task. This model and various metadata (hyperparameters, featurization, normalization applied to the input, class to integer label dictionary, version of URL Text Module, etc.) are saved for use in future inferencing. An example of inferencing on unseen Japanese text is shown at the bottom of the notebook where the model predicts Human Risk/No Human Risk on Japanese RiskMap reports from Typhoon Hagibis in 2019.
- Directory: [./Classification]()
- Notebook: [./Classification/FC_txt_data_classification.ipynb]()
- Misc: 
    * Associated plots from the Human Risk Classification experiments (Nested CV results, confusion matrix of SVM model, per-class performance of SVM model, and precision-recall curve of SVM model) can be found [here]()
    * The Human Risk SVM model fitted on the entire dataset and its corresponding metadata can be found [here]().

### **Clustering of Fukuchiyama Crisis Text Data**
---
5. **Clustering the FC Firefighter Text Reports to uncover human-interpretable, semantically-similar categories across the corpus for future classification tasks & labels:**

**Create TF-IDF and BERT with CLS Pooling Embeddings**

* Creates TF-IDF (based on unigrams) vectors of all of the reports (or documents) in the dataset using the tokenized documents from step 3. Also makes use of the BERT with CLS pooling embeddings from step 3. These featurizations of the input text are normalized with a StandardScaler construct from scikit-learn.

**Generate WCSS plots for Different Hyperparameter Combinations & Selection of the Query Subset for Qualitative Investigation**
* For $K$ values from 2 to 20, the Within-Cluster Sum-of-Squares (WCSS) plot, or the "Elbow" plot, is plotted for each unique combination of the following configuration parameters:
    - **Featurization type (one of):** {BERT Embeddings, TF-IDF Embeddings}
    - **Dimensionality Reduction Technique (one of):** {PCA (2 components), t-SNE (2 components), No Dimensionality Reduction}
    - **Clustering Algorithm (one of):** {K-means, K-medoids}
    
Therefore 12 elbow plots are generated and saved (one for each combination of the configuration parameters above)

From these plots, a subset of hyperparameter combinations are selected for futher qualitative investigation. These combinations were selected if both:
 
 1. There was an elbow in the plot
 2. If the WCSS scores across $K$-values were relatively lower compared to the other hyperparameter combinations

 For each of these selected hyperparameter combinations, a $K$ value was selected at which the "Elbow" occurs in the plot. This resulted in the following hyperparameter combinations in the query subset for further qualitative investigation:

 * BERT Embeddings, No Dimensionality Reduction, & K-medoids (12 cluster)
 * BERT Embeddings, PCA (2 components), & K-medoids (9 clusters)
 * BERT Embeddings, t-SNE (2 components), & K-medoids (9 clusters)
 * TF-IDF Embeddings, PCA (2 components), & K-medoids (8 clusters)
 * TF-IDF Embeddings, t-SNE (2 components), & K-medoids (14 clusters)  

**Qualitative Investigation of each Combination in the Query Subset**

For each of the hyperparameter combinations in the query subset above, the following auxillary outputs are computed:

1. A plot of the clustering of the embeddings in 2D space if a dimensionality technique was applied prior to being clustered, color-coded by cluster ID.
2. For each cluster:
    1. An ordered list is generated of the 20 (or less if there was less than 20 data points in the cluster) closest data points (by euclidean distance) to the cluster center showing the distance value, the original Japanese text, and the corresponding English translation

Note: Since these outputs showed the raw text data which we've been asked not to share, we are unable to provide those outputs in the notebook

The qualitative evalution occured by looking at the English translations of the documents closest to each cluster center and answering the question: **When looked at together, does the
content of the representative documents in a cluster elicit an interpretable
label?**

The hyperparameter combination selected for the final evaluation below was determined by having the highest number of clusters which answered "Yes" to this question, i.e. combination which gave the most coherent clustering across clusters, namely **BERT Embeddings, t-SNE (2 components), & K-medoids (9 clusters)**
     
**Final Qualitative Evaluation of Clustering of FC Firefighter Reports by Fluent Japanese Speaker**

For the hyperparameter combination:  **BERT Embeddings, t-SNE (2 components), & K-medoids (9 clusters)**, the notebook generated a color-coded plot of the clustered data in 2D, and generated a CSV showing the original Japanese text report and the corresponding English translations of the 20 closest data points to each cluster center ordered by distance. Additionally, another CSV was generated showing the top 20 unigrams of each cluster ordered by TF-IDF score which was computed for the cluster-level document corpus, in which each cluster is represented by a document which is the concatenation of the tokenized documents that were assigned to that cluster.

Note: Similar to the above, since these outputs showed the raw text data which we've been asked not to share, we are unable to provide those outputs in the notebook.

A member of the Urban Risk Lab who is fluent in Japanese & English assigned a human-interpretable label to each cluster using the CSVs mentioned above. The resulting mapping from cluster ID to human-assigned label is the following:

```
cluster_category_names = {
    0: 'Rescue (activites/requests)',
    1: 'Road Closure by the City',
    2: 'River Water Level and Corresponding Warning for EOC/FD',
    3: 'Impassable Roads (due to flood/obstacles/damage)',
    4: 'Residential Areas/Buildings in Flood (Risk)',
    5: 'Landslide/Fallen Tree',
    6: 'FD Activities/Weather Warning/Flood Control Alert',
    7: 'Areas with Flood Risk',
    8: 'Areas where FD activities are happening'
}
```
- Directory: [./Clustering]()
- Notebook: [./Clustering/FC_txt_data_clustering.ipynb]()
- Misc:
    * The WCSS, or "Elbow" plots for each hyperparameter combination can be found [here]()
    * The labeled plot of the clustering found for the hyperparameter combination of BERT Embeddings, t-SNE (2 components), & K-medoids (9 clusters) can be found [here]()