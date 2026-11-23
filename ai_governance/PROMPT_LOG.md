
Prompt Log (Done with Claude)

Entry 1 : Checking the dataset (Alix)
I asked the AI if our dataset was good, and I only sent the CSV file. This prompt was too vague. A better prompt would describe the data (30 features, target) and ask for specific checks: missing values, class balance and exact duplicates. I re-ran these checks myself in notebook 01. I found 5,205 duplicates, while the AI first said 5,269.

Entry 2 : Data exploration (Alix)
I asked the AI to start the data exploration without giving any rules. A better prompt would say: drop the Index column, remove duplicates before any split, check if the encoding is the same for every feature, and do not select features on the full dataset to avoid data leakage. I checked the duplicate counts, the class balance after deduplication (52% phishing and 48% legitimate) and the features with an inconsistent encoding.


Entry 3 : Baseline (Lou-Ann)
I asked the AI to do week 2 without saying which model, split or metric to use. A better prompt would ask for a majority-class baseline and a logistic regression in a Pipeline, an 80/20 stratified split, 5 fold cross-validation on the training set only, and recall as the main metric, without ever using the test set. If the recall target (95% ) is not reached, the plan is to adjust the decision threshold or try other models in week 3. I checked that the split is stratified and that the test set is never used.

Entry 4 : Week 3 plan and notebook 05 (Lou-Ann)
My first prompt was bare: "Tell me exactly what we have to do for week 3 and how to do it." The AI gave a generic plan that did not match our project (wrong notebook names, test evaluation planned too early). I then gave it access to our repository so that it could compare our notebooks with the guidelines. It helped me identify what was still missing (ensemble learning, an out-of-course model, a statistical comparison with the baseline) and gave me a code draft for notebook 05. I used this draft as a starting point and audited it: I checked that the test set is never used, that all models are compared on the same folds, and that the statistical test is valid for cross-validation scores (a classic t-test assumes independent scores, so we use the corrected resampled t-test of Nadeau & Bengio, 2003, with Wilcoxon as a fallback). I chose [YOUR OWN CHANGE, e.g. the MLP grid / the metric used for the tests], wrote the explanations myself, and checked on Google Scholar that the reference paper (Grinsztajn et al., NeurIPS 2022) exists.