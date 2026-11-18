
Prompt Log

Entry 1 : Checking the dataset (Alix)
Original prompt: "is this dataset good?" + CSV file
Improved prompt: "Load phishing.csv. Report missing values, class balance and exact duplicates (features + label)."
What I checked: I re-ran the counts in notebook 01.

Entry 2 : Data exploration (Alix)
Original prompt: "let's start"
Improved prompt: "Write a data exploration notebook. Drop Index, remove exact duplicates before any split, and do not select features on the full dataset (data leakage)."
What I checked: duplicate counts and class balance after deduplication.

Entry 3 : Baseline (Alix)
Original prompt: "let's do week 2"
Improved prompt: "Build a majority-class and a logistic regression baseline in a Pipeline. Use an 80/20 stratified split with a fixed seed, 5-fold CV on the training set only, and report recall, precision, F1 and ROC-AUC."
What I checked: the test set is never used and the split is stratified.