# Jigsaw-Unintended-Bias-in-Toxicity-Classification
A complete analysis + model for the competition hosted on Kaggle by Conversation AI - A research initiative founded by Jigsaw and Google

# About the problem
The Conversation AI team, a research initiative founded by Jigsaw and Google (both part of Alphabet), builds technology to protect voices in conversation. A main area of focus is machine learning models that can identify toxicity in online conversations, where toxicity is defined as anything rude, disrespectful or otherwise likely to make someone leave a discussion.

Last year, in the Toxic Comment Classification Challenge, you built multi-headed models to recognize toxicity and several subtypes of toxicity. This year's competition is a related challenge: building toxicity models that operate fairly across a diverse range of conversations.

# Previous competition and it's problem
Here’s the background: When the Conversation AI team first built toxicity models, they found that the models incorrectly learned to associate the names of frequently attacked identities with toxicity. Models predicted a high likelihood of toxicity for comments containing those identities (e.g. "gay"), even when those comments were not actually toxic (such as "I am a gay woman"). This happens because training data was pulled from available sources where unfortunately, certain identities are overwhelmingly referred to in offensive ways. Training a model from data with these imbalances risks simply mirroring those biases back to users.

In this competition, you're challenged to build a model that recognizes toxicity and minimizes this type of unintended bias with respect to mentions of identities. You'll be using a dataset labeled for identity mentions and optimizing a metric designed to measure unintended bias. Develop strategies to reduce unintended bias in machine learning models, and you'll help the Conversation AI team, and the entire industry, build models that work well for a wide range of conversations.

# To understand more on bias
https://www.youtube.com/watch?v=59bMh59JQDo

# Understanding the evalution metrics
https://medium.com/jash-data-sciences/measuring-unintended-bias-in-text-classification-a1d2e6630742

a. Subgroup AUC — This calculates AUC on only the examples from the subgroup. It represents model understanding and performance within the group itself. A low value in this metric means the model does a poor job of distinguishing between toxic and non-toxic comments that mention the identity.

b. BNSP AUC — This calculates AUC on the positive examples from the background and the negative examples from the subgroup. A low value here means that the model confuses toxic examples that mention the identity with non-toxic examples that do not.

c. BPSN AUC — This calculates AUC on the negative examples from the background and the positive examples from the subgroup. A low value in this metric means that the model confuses non-toxic examples that mention the identity with toxic examples that do not.

d. Final Metrics — We combine the overall AUC with the generalized mean of the Bias AUCs to calculate the final model score:

score=w0AUCoverall+∑a=1AwaMp(ms,a) where:

A = number of submetrics (3)

ms,a = bias metric for identity subgroup s using submetric a

wa = a weighting for the relative importance of each submetric; all four w values set to 0.25
