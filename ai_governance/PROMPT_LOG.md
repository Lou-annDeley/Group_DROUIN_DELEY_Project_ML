
Prompt Log

Entry 1 : Checking and exploring the dataset (Alix)
I asked the AI if our dataset was good, then to start the exploration, without giving any rules. A better prompt would describe the data and ask for clear checks: missing values, class balance, exact duplicates, and no feature selection on the full dataset. I re-ran the checks in notebook 01 and found 5,205 duplicates, while the AI first said 5,269.

Entry 2 : Baseline (Alix)
I asked the AI to "do week 2" without saying which model, split or metric to use. A better prompt would ask for a majority-class baseline and a logistic regression in a Pipeline, an 80/20 stratified split, 5-fold CV on the training set only, and recall as the main metric. I checked that the split is stratified and that the test set is never used.

Entry 3 : Week 3 plan (Lou-Ann)
My first prompt was: "Tell me exactly what we have to do for week 3 and how to do it." The answer was generic and planned the test evaluation too early. I then gave the AI access to our GitHub repository and asked it to compare our notebooks with the guidelines. It found that requirements.txt was empty and that ensembles and an out-of-course model were missing. We fixed this ourselves.

Entry 4 : Models and final evaluation (Alix)
I asked the AI to do weeks 3 and 4 without giving precise rules. When it started the test evaluation, I noticed that notebook 05 was not done yet, so the final model would have been chosen after seeing the test set. A better prompt would be: "Compare all models with cross-validation, choose the final model, and only then evaluate it once on the test set." I re-ran notebook 03 and got the same scores.

Entry 5 : Feature selection and MLP (Lou-Ann)
I used constrained prompts to review notebooks 04 and 05. In the first one, I described our data and methods, then wrote: "Check that no selection step sees the validation folds." and "Do not use the test set." In the second one, I wrote: "I will cite Grinsztajn et al. (NeurIPS 2022): summarise its main finding in two sentences, and do not invent any other reference." I checked that every selection step is inside the Pipeline and that the paper exists.

Entry 6 : Statistical tests and final evaluation (Lou-Ann)
I asked the AI to check our statistics. One prompt asked: "Check my statistical comparison: is the corrected resampled t-test of Nadeau & Bengio (2003) correctly implemented below, with the right n_test/n_train ratio?" Another one started with: "My final model is a Gradient Boosting chosen with cross-validation on the training set only." and asked if the test set is used only once and if the bootstrap confidence intervals are correct. I checked that the ratio is 1/4 for 5-fold CV and that test.csv is only loaded in notebook 06.