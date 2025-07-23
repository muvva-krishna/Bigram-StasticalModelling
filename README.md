### **Bigram Character-Level Name Generation: A Tale of Two Approaches**

This project demonstrates two methods for generating new Indian names by learning from a list of 53,982 existing names. The first approach is purely statistical, while the second uses a simple neural network. Ultimately, both methods produce the same results, showcasing how a basic neural network can replicate a classical statistical model.

---
### **Approach 1: The Statistical Model**

This method relies on directly counting character co-occurrences and normalizing them into probabilities.

* **Logic**:
    * The model processes each name by adding a start `(<S>)` and end `(<E>)` token.
    * It then builds a 28x28 matrix to count the frequency of every possible character pair (bigram). For example, it counts how often 'a' is followed by 'n'.
* **Generation**:
    * The raw counts in the matrix are converted into probabilities by normalizing each row.
    * To generate a name, the model starts with `<S>` and iteratively samples the next character based on these learned probabilities until `<E>` is chosen.
* **Evaluation**:
    * The model's accuracy is measured by its average **Negative Log-Likelihood (NLL)**, which was **2.1748** on the dataset. A lower NLL is better.
    * As a test, the non-Indian name "roberts" yielded a much higher NLL of **3.5319**, confirming the model learned patterns specific to the training data.

---
### **Approach 2: The Neural Network Model**

This approach frames the problem as a simple classification task: predicting the next character in a sequence.

* **Architecture**:
    * A single-layer neural network multiplies a one-hot encoded input character by a 28x28 weight matrix (`W`).
    * A **softmax** function is applied to the output to create a probability distribution for the next character.
* **Training**:
    * The network is trained using gradient descent for 300 epochs.
    * The loss function is the **Negative Log-Likelihood (NLL)**. The network adjusts its weights (`W`) to minimize this loss, effectively learning the character transition probabilities.
    * The final loss after training was **2.1929**.

---
### **Key Insight: The Two Models are Identical**

The simple neural network is mathematically equivalent to the statistical model.
* The weight matrix `W` in the neural network effectively learns the log-counts of the bigrams.
* The **softmax** function is the neural network's way of normalizing counts into a probability distribution.

By minimizing the NLL loss, the neural network converges to the same probability model derived from direct statistical counting.

### **Results Comparison**

Because the underlying models are the same, both notebooks produce identical outputs when given the same random seed.

| Model Approach | Average Negative Log-Likelihood |
| :--- | :--- |
| Statistical | **2.1748** |
| Neural Network | **2.1929** (Final loss) |

**Generated Names (from both models):**
* mik
* rabal
* maanek
* ishiya
* kahel
* abamathanaeraya
* ka
* savithrnan
...and so on.
