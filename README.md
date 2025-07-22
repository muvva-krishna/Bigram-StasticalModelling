This project builds a simple character-level bigram language model trained on a dataset of Indian names. The model learns character sequence patterns to generate new, stylistically similar names.

***

### **Methodology**

1.  **Data Preparation**: A list of names from `Indian_Names.txt` is loaded and processed. Special start (`<S>`) and end (`<E>`) tokens are added to each name to signify its beginning and end.

2.  **Bigram Counting**: The model counts all adjacent pairs of characters (bigrams) across the dataset to learn which characters are likely to follow others.

3.  **Probability Modeling**: The bigram counts are stored in a 2D `PyTorch` tensor and converted into a probability distribution. This allows the model to predict the next character based solely on the previous one.

4.  **Name Generation**: New names are generated character-by-character. Starting with the `<S>` token, the model samples the next character based on the learned probabilities and continues until an `<E>` token is generated.

5.  **Evaluation**: The model's performance is measured using **Negative Log Likelihood (NLL)**. A lower NLL indicates that the model is better at predicting the names in the dataset.

***

### **Results**

* The model successfully generates plausible Indian-sounding names .
* The NLL for the training data was approximately **2.17**. When tested on a non-Indian name ("roberts"), the NLL was significantly higher (**3.53**), confirming the model learned patterns specific to the dataset.
* A visualization of the bigram count matrix clearly shows the learned character relationships.
