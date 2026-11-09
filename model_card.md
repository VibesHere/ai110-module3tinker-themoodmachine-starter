# Model Card: Mood Machine

This model card is for the Mood Machine project, which includes **two** versions of a mood classifier:

1. A **rule based model** implemented in `mood_analyzer.py`
2. A **machine learning model** implemented in `ml_experiments.py` using scikit learn

You may complete this model card for whichever version you used, or compare both if you explored them.

## 1. Model Overview

**Model type:**  
Describe whether you used the rule based model, the ML model, or both.  
Example: “I used the rule based model only” or “I compared both models.”
I compared both models. The rule based model regularly made errors based on the inability to pick up on tone or sentiment.

**Intended purpose:**  
What is this model trying to do?  
Example: classify short text messages as moods like positive, negative, neutral, or mixed.
The models attempt to classify the feelings within a message as positive, negative, neutral, or mixed.

**How it works (brief):**  
For the rule based version, describe the scoring rules you created.  
I implemented rules that add or subtract from a score based on the content of the text itself, producing a result based on the difference or end state.

For the ML version, describe how training works at a high level (no math needed).
It creates a model to train from based on the content of the text and their results, and then tries to predict it based on it's model.



## 2. Data

**Dataset description:**  
Summarize how many posts are in `SAMPLE_POSTS` and how you added new ones.
There are 11 posts, I added 6 of them.


**Labeling process:**  
Explain how you chose labels for your new examples.  
Mention any posts that were hard to label or could have multiple valid labels.
I created the examples with a sentiment or expression in mind. A satirical or ironic comment like "I just love staying late at work" could be genuine if someone loves their work, however not everyone does and often staying late means missing out on plans.

**Important characteristics of your dataset:**  
Examples you might include:  

- Contains slang or emojis  
- Includes sarcasm  
- Some posts express mixed feelings  
- Contains short or ambiguous messages

My dataset includes sarcasm, short messages, and uncommon language. 

**Possible issues with the dataset:**  
Think about imbalance, ambiguity, or missing kinds of language.
It doesn't include emojis, or ambiguous messages that inherently have no meaning. 

## 3. How the Rule Based Model Works (if used)

**Your scoring rules:**  
Describe the modeling choices you made.  
Examples:  

- How positive and negative words affect score  
- Negation rules you added  
- Weighted words  
- Emoji handling  
- Threshold decisions for labels

**Strengths of this approach:**  
Where does it behave predictably or reasonably well?

**Weaknesses of this approach:**  
Where does it fail?  
Examples: sarcasm, subtlety, mixed moods, unfamiliar slang.

## 4. How the ML Model Works (if used)

**Features used:**  
Describe the representation.  
Example: “Bag of words using CountVectorizer.”

**Training data:**  
State that the model trained on `SAMPLE_POSTS` and `TRUE_LABELS`.
It trained on Sample Posts and it's labels

**Training behavior:**  
Did you observe changes in accuracy when you added more examples or changed labels?
Accuracy seemed unchanged. 

**Strengths and weaknesses:**  
Strengths might include learning patterns automatically.  
Weaknesses might include overfitting to the training data or picking up spurious cues.

Its overfitted and gets 100% as the training data is the same as the testing data. This can cause errors when presented with new information. The ML model seems to at least report a higher score compared to the scoring model, as anything similar to the training data gets a similar result. 



## 5. Evaluation

**How you evaluated the model:**  
Both versions can be evaluated on the labeled posts in `dataset.py`.  
Describe what accuracy you observed.
The ML model is perfectly accurate on the data it receives. The scoring model will make mistakes not immediately clear based on the context of the text. 


**Examples of correct predictions:**  
Provide 2 or 3 examples and explain why they were correct.

**Examples of incorrect predictions:**  
Provide 2 or 3 examples and explain why the model made a mistake.  
If you used both models, show how their failures differed.

When comparing "I love staying late at work" as a good example, the ML model recognized this from the training and correctly predicted it. The scoring model has never seen the text before and simply tries to identify it based on the content. If the training data were loaded with satire, the scoring model would be very wrong, and the ML model would start mixing up non-factual information with identical factual information. 

## 6. Limitations

Describe the most important limitations.  
Examples:  

- The dataset is small  
- The model does not generalize to longer posts  
- It cannot detect sarcasm reliably  
- It depends heavily on the words you chose or labeled

The dataset IS small, and the scoring model depends heavily on the thesaurous of categorized emotion. Longer posts aren't necessarily an issue until the descriptive words contradict each other, like describing good and bad at the same time. 

## 7. Ethical Considerations

Discuss any potential impacts of using mood detection in real applications.  
Examples: 

- Misclassifying a message expressing distress  
- Misinterpreting mood for certain language communities  
- Privacy considerations if analyzing personal messages

A message can easily be misinterpreted or misclassified when you don't understand the full context. Even in seemingly public settings like online, analyzing people's feelings without their knowledge can be invasive. Someone who uses a word wrong can end up in the wrong category, or worse an oversight can cause a word to be classified wrong and falsely flag the data. 

## 8. Ideas for Improvement

List ways to improve either model.  
Possible directions:  

- Add more labeled data  
- Use TF IDF instead of CountVectorizer  
- Add better preprocessing for emojis or slang  
- Use a small neural network or transformer model  
- Improve the rule based scoring method  
- Add a real test set instead of training accuracy only

More labeled data. 
Undefined words or """characters""" could be distilled if listed alongside similar words, allowing the scoring model to add to it's dictionary of words. As opposed to manually adding words to those lists, and to support the creation of new slang.
A real test would actually clarify how the models perform. 