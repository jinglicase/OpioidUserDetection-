# Detection of Opioid Users from Reddit Posts via an Attention-based Bidirectional Recurrent Neural Network

## Introduction

This is a companion site for our paper entitled "Detection of Opioid Users from Reddit Posts via an Attention-based Bidirectional Recurrent Neural Network". The primary purposes of this site are to 1) provide the manually labeled dataset used in the paper, and 2) provide code used in generating the results in the paper.  

## Dataset

Our data was collected from Reddit using Python Reddit API Wrapper (PRAW), a web crawling tool. The data was obtained from three subreddits called 'Opiates', 'OpiatesRecovery', and 'Drugs'. For each subreddit, we collected the comments of redditors who were in the "Top-Month" tab from January 6th 2020 to February 5th 2020. The collection was based on opioid-related keywords (e.g., opium, opioid) as well as their slang words (e.g., black, chocolate). All comments from the same redditor were concatenated into one ``post'', representing the user. 

The initial dataset had no labels. The label of each user/post was obtained manually by crowdsourcing with the help of 34 students in a data mining class. Each post was read by two students independently and was assigned to one of five possible labels. If the labels from the two students were the same, that label was used for the post/redditor. Otherwise, a third student read it again and provided her/his own result. The label with two votes was deemed the correct one. The five labels are: non-opioid users, opioid users, previous opioid users (who actually quit now),  drug dealers, and users who use prescription drugs. Their corresponding numbers of posts/redditors are  410, 471, 107,  27, 43, respectively. Because the total number of redditors in the last three categories was relatively small, in the current study, we only focused on the first two cases which contained 881 users (the file is dataCollection\data-withoutID-2.csv). 


## Quick Start

To run the proposed models, make sure that you follow the steps below: 

1. Ensure your Python version is above 3.0, Tensorflow (2.2.0), Keras (2.3.1).
	
2. Creat a file folder named "embedding_glove".
	
3. Download “glove.6B.zip” from website https://nlp.stanford.edu/projects/glove/. Extract this file in the folder “embedding_glove”.
	
4. The main file is "biWordEmbeddingModify.py". You can modify hyperparameters, including max_length, embeddingDim, variantName, in the main function. Specifically, embeddingDim can be chosen as 50, 100, 200, 300. VariantName can be from "variant1" to "variant6", which is corresponding to the six model variants in the paper. The max_length parameter was chosen as 100 in the paper.
	
5. The comparing methods are implemented in the file "comparisonBi.py".

## How to get the results in our paper?

1. Table 1: Run slangOccupatioin.py to get the result.

2. Table 2: The keywords are generated based on the attention matrix. The attention matrix is generated as the parameter "att_pred" in the getResult method in biWordEmbeddingModify.py.
    
3. Figure 2: Run drawSentenceLength.py to get the result.

4. Figure 3: The loss was obtained during the training process in biWordEmbeddingModify.py.

5. Figure 4: Results using different dimensions of word vectors were obtained in biWordEmbeddingModify.py.
    
6. Figure 5: Modify hyperparameters to get the data by biWordEmbeddingModify.py.

7. Figure 6: Run drawWordCloud.py to get the result. The list "imp_list" can be get as the result "OrderedDict" which is generated by running biWordEmbeddingModify.py.
    
## How to run the code on your own data?

You can generate your own data as a CSV file. The column names are "student1", "student2", "consensus", "userID",  "content", and "keywords".
"student1" represents judgement of the first student. "0" represents that the student did not consider the author of this post as drug user while "1" represents that the student considered the author of this post as drug user.
"student2" is as same as "student1" except it is from the second student.
"consensus" represents the final judgement of "student1" and "student2". if they can not get consensus, the third student would make the final judgement.
"userID" represents the ID of the user of this post.
"content" represents the content of the posts.
"keywords" represents the words appeared both in the posts and the paper "Drug Slang Code Words". The ormat of "keywords" is like "opiate^opiates^china". The keywords are joined together using "^".
    
After generating the CSV file, put this file into the "dataset1000" folder. Meanwhile, "data-withoutID-2.csv" in each code should be replaced by the name you give for your own file.
