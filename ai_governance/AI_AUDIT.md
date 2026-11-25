AI Audit – Catch & Correct

Flaw 1 – Wrong number of duplicates (caught by Alix)

When we asked the AI to profile the dataset, it reported 5,269 duplicate rows. When we checked this number in our own notebook, we found only 5,205 exact duplicates. The AI compared the 30 features only and ignored the label, so websites with the same features but different labels were also counted as duplicates. These rows are not true duplicates: they are conflicting examples. We fixed the count by checking duplicates on the features and the label together. Notebook 01 now shows 5,205 exact duplicates and, separately, 64 conflicting feature combinations.

Flaw 2 – Test evaluation planned too early (caught by Lou-Ann)

When I asked the AI for a week 3 plan, it proposed a generic plan that evaluated the final model on the test set in week 3, before the ensemble models and the out-of-course model were tested. If we had followed it, we would have seen the test results before choosing the final model, and any later change of model would have been biased by the test set. The AI did not know our project and followed a generic order of steps. We fixed this by keeping the test set for a single evaluation in week 4, after all models were compared with cross-validation. Notebook 06 is the only notebook that loads test.csv.

Flaw 3 – Wrong majority-class baseline (caught by Alix)

The AI stated that the majority-class baseline would always predict "legitimate" and reach about 56% accuracy. This was true for the raw dataset, but not after removing duplicates: phishing then becomes the majority class (51.6%). The AI used the class balance computed before deduplication. We fixed this by computing the class balance again on the deduplicated data. Notebook 02 confirms that the baseline always predicts phishing, with a recall of 1.0 and a precision of 0.516.

Flaw 4 – Optimistic score for the neural network (caught by Lou-Ann)

In notebook 05, the AI tuned the MLP hyperparameters with a grid search on the training set, then measured its score with cross-validation on the same training set. The same data was used to choose the hyperparameters and to evaluate the model, so the score is a bit optimistic. I fixed this with nested cross-validation: the grid search runs inside each outer fold, so each outer validation fold is never used to choose the hyperparameters. The nested ROC-AUC is 0.980 ± 0.005, against 0.982 without nesting. The bias is small, and the conclusion does not change: the MLP stays clearly below Gradient Boosting (0.993).

Flaw 5 – Wrong encoding assumption (caught by Alix)

The AI assumed that all features follow the same order, with −1 meaning a phishing sign, 0 suspicious and 1 a legitimate sign, as written in the dataset description. When we checked the correlation of each feature with the target, we found that 10 features are positively correlated with phishing, so for them the encoding works the other way round. The AI trusted the dataset documentation without checking it against the data. We now check the sign of the correlation before interpreting a feature. Section 6 of notebook 01 lists these 10 features, and we note this as a limitation in the report.

Flaw 6 – L1 stability not informative (caught by Lou-Ann)

In notebook 04, the AI measured the stability of the L1 selection with C = 0.03. With this value, 12 features were selected in 100% of the bootstrap samples, so the stability could not tell them apart and was not useful for the final ranking. The AI chose a penalty that was too weak for this purpose. I tested smaller values of C: with C = 0.005, only 3 features are always selected (AnchorURL, HTTPS and ServerFormHandler), and 6 others are selected sometimes. This gives a clearer ranking, and it matches the other methods.

Flaw 7 – Test set evaluated before the final model was chosen (caught by Alix)

In week 4, the AI started the final evaluation on the test set (notebook 06) while notebook 05 was not done yet. If notebook 05 had found a better model, we would have chosen the final model after seeing the test results, which is a form of data leakage. The AI followed the week order without checking that model selection was finished. We ran notebook 05 first: it compares all models with repeated cross-validation and chooses Gradient Boosting. Only then was notebook 06 run on the test set.

Flaw 8 – Wrong statement about scikit-learn (caught by Alix)

The AI wrote that penalty="l1" no longer works in recent versions of scikit-learn. This is wrong: the parameter is deprecated, so it still works but shows a warning and will be removed in version 1.10. The AI confused "deprecated" and "removed". We fixed the comment in notebook 04 and used l1_ratio=1, the recommended replacement. Running penalty="l1" with scikit-learn 1.9.1 shows a FutureWarning, not an error.