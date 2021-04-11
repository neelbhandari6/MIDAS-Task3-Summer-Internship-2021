# MIDAS-Task3-Summer-Internship-2021
Welcome to the Task3 submission by Neel Bhandari

I have 4 specific tasks that I have focussed on :
1. Data Cleaning
2. Data Exploration and Visualisation
3. Model development for category prediction
4. Future work

The notebook focusses on all 4 parts.
The models I have used include:
On TF-IDF:
  1. Naive Bayes
  2. KNearest Neighbours Classifier
  3. Random Forest
  4. SVM
  5. Logistic Regression
  6. Stacked Classifier: Could not implement yet.

On Embeddings:
  1. LSTM

For each model, I have provided a detailed intuition behind my use of it, an interpretation of the results based on research and why I compared it with other models.

Let's go into a detailed description of all the subtasks:
## 1. Data Cleaning:
The first task in hand was dealing with redundant features within the dataset. This includes the unique ID's, URL column etc. For each column, I have provided a detailed explaination on why I have dropped them, either using research or statistically proving their irrelevance comapred to other, more comprehensive columns present.

This was an integral part of the process, as it allows us to remove redundencies that may harm model performance by introducing noise to the data.
Further cleaning, as described below, was done on intuitively important columns using either statistical methods or visualisation

## 2. Data Exploration and Visualization
I first looked at the retail price and discounted_price column. to optimise the representation of the data, I converted both of the columns to a discount% column. This meant it was a more clean dataset.

I then looked at the contribution of the product name and the product brand and their contribution to the dataset. On preliminary analysis, it was seen that the columns seemed similar to the description column. On further introspection by analysing their presence in the description column, it was seen that the product name was already present in 99.975% of the simultaneous description data. This meant it's absence had minimal contribution to the dataset overall and was discarded.
With respect to the brand column, it was seen there were over a 1000 description values that did not mention the brand name. This was seen as a significant feature that may be missed, and the 1000 brand names were appended to the product description

This brings us to the class distribution in the category_tree column. Here are the results of the presence of these classes
#### Presence of primary category values.
<img width="575" alt="Screenshot 2021-04-11 at 9 50 19 PM" src="https://user-images.githubusercontent.com/30409992/114312321-ebee2680-9b0f-11eb-9471-954f145c01b7.png">

#### Presence of secondary category values.
<img width="573" alt="Screenshot 2021-04-11 at 9 51 19 PM" src="https://user-images.githubusercontent.com/30409992/114312367-0e803f80-9b10-11eb-8b66-f64ae732d8ae.png">

#### Presence of third category values.
<img width="566" alt="Screenshot 2021-04-11 at 9 51 59 PM" src="https://user-images.githubusercontent.com/30409992/114312396-25bf2d00-9b10-11eb-8787-6ebfe14befdb.png">

As can be seen, only the primary and secondary categories hold significant data to be worked with, with the secondary category being considered due to the diversity of presence of non-empty labels.
The reason to select secondary category was also to experiment and see the output with our models.

Post cleaning the columns, here's what some of the visualizations looked like:

#### Word clouds for interactive feature analysis
<img width="474" alt="Screenshot 2021-04-11 at 9 55 05 PM" src="https://user-images.githubusercontent.com/30409992/114312536-95cdb300-9b10-11eb-95b6-f3e42d7f907c.png">
<img width="725" alt="Screenshot 2021-04-11 at 9 54 49 PM" src="https://user-images.githubusercontent.com/30409992/114312501-8babb480-9b10-11eb-882c-fefc1c7f9bfa.png">  

#### Text Length in Characters:
<img width="685" alt="Screenshot 2021-04-11 at 9 55 25 PM" src="https://user-images.githubusercontent.com/30409992/114312559-a120de80-9b10-11eb-9fa8-4582edbbbba1.png">

#### Text Length in Words
<img width="646" alt="Screenshot 2021-04-11 at 9 55 55 PM" src="https://user-images.githubusercontent.com/30409992/114312579-b3028180-9b10-11eb-8fec-1245b199debb.png">

#### Label Distribution in Primary category
<img width="1060" alt="Screenshot 2021-04-11 at 9 57 10 PM" src="https://user-images.githubusercontent.com/30409992/114312627-dfb69900-9b10-11eb-863c-d060d82c3d6f.png">

#### Label Distribution in Secondary Category
<img width="781" alt="Screenshot 2021-04-11 at 9 58 01 PM" src="https://user-images.githubusercontent.com/30409992/114312657-fe1c9480-9b10-11eb-9ee0-ca47abd8bd06.png">

This provides us with a comprehensive overview of the features present and their distribution. This also provides us important details for feature optimization in the models we will use in the future.

## 3. Model development for category prediction

### Models with Primary Category
We start with using TF-IDF for the baseline model, a simplistic and suprisingly successful weight assignment algorithm that allows for important features to get higher weights, and hence more weight in the categorization process.

Using TF-IDF on product description and primary categories, we analyse with different classifiers:(All detailed reports are in the notebook)
Multinomial Naive Bayes : 0.91 F1 Score
SVM: 0.99 F1 score
KNN Classifier: 0.94 accuracy
Random Forest: 0.92 accuracy
Stacking Classifier: Could not implement.

LSTM using Keras Embedding: 0.95 Validation Accuracy

<img width="643" alt="Screenshot 2021-04-11 at 10 21 10 PM" src="https://user-images.githubusercontent.com/30409992/114313454-3a052900-9b14-11eb-8dd2-a991b06ea271.png">

We also analysed the effect of Discount on Category prediction: 0.41 F1 Accuracy.
Given low correlation, we removed the discount column from further use.

### Models with Secondary Category
TF-IDF and SVM: 0.87 F1 accuracy
LSTM and Keras Embedding: 0.935 Validation accuracy

<img width="650" alt="Screenshot 2021-04-11 at 10 23 06 PM" src="https://user-images.githubusercontent.com/30409992/114313529-7f295b00-9b14-11eb-9ae5-588e0b4d73c1.png">

## Future Work:

There are several approaches we can explore based on my preliminary research.
1. Deep Neural Networks: It would be interesting to analyse the effectiveness of training this data over a considerable number of layers in a neural network, and compare the performance with LSTM to further interpret the applicability of long term dependancies in this dataset.
2. Transformers: Attention has changed the landscape of NLP. Given that they are non sequential, the long term dependancy issue does not take place if present, but moreover self-attention and positional embeddings are interesting concepts that may have an impact on larger datasets.
3. Self-Supervised Learning: This has always interested me and is definitely a mechanism to be explored. The ability for self-supervised learning to explore semantic relationships has been shown before,and through clustering methods, it would be interesting to explore this
4. Meta -learning for few shot classification: Learning to learn is the basis of meta learning, and reducing this task to a few shot prediction would be immensely beneficial.













