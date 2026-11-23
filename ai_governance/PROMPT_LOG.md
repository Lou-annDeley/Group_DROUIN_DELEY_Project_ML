
Prompt Log (Done with Claude)

Entry 1 : Checking the dataset (Alix)
I asked the AI if our dataset was good, and I only sent the CSV file. This prompt was too vague. A better prompt would describe the data (30 features, target) and ask for specific checks: missing values, class balance and exact duplicates. I re-ran these checks myself in notebook 01. I found 5,205 duplicates, while the AI first said 5,269.

Entry 2 : Data exploration (Alix)
I asked the AI to start the data exploration without giving any rules. A better prompt would say: drop the Index column, remove duplicates before any split, check if the encoding is the same for every feature, and do not select features on the full dataset to avoid data leakage. I checked the duplicate counts, the class balance after deduplication (52% phishing and 48% legitimate) and the features with an inconsistent encoding.


Entry 3 : Baseline (Lou-Ann)
I asked the AI to do week 2 without saying which model, split or metric to use. A better prompt would ask for a majority-class baseline and a logistic regression in a Pipeline, an 80/20 stratified split, 5 fold cross-validation on the training set only, and recall as the main metric, without ever using the test set. If the recall target (95% ) is not reached, the plan is to adjust the decision threshold or try other models in week 3. I checked that the split is stratified and that the test set is never used.

Entry 4 : Week 3 review of our repository (Lou-Ann)
My first prompt was bare: "Tell me exactly what we have to do for week 3 and how to do it." The AI answered with a generic plan that did not match our project: it used notebook names we did not have and planned the final test evaluation for week 3, while we keep it for week 4. I then gave the AI read access to our GitHub repository and asked it to compare our real notebooks with the project guidelines, without using the test set. With this context, the answer became specific: it found that requirements.txt was empty, that CONTRIBUTIONS.md had a wrong file path and described work we had not done (calibration, test-set evaluation), and that two parts of Step 3 were still missing: ensemble learning and an out-of-course model justified by a scientific paper. We fixed requirements.txt and CONTRIBUTIONS.md ourselves. Our week 3 work is in notebook 03 (tuning of the course models, overfitting check, decision threshold for 95% recall, error analysis) and notebook 04 (feature selection with filter, wrapper and embedded methods). We decided to add the ensemble models and the out-of-course model in week 4, in a separate notebook, before the single evaluation on the test set.