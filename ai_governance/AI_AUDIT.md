Flaw 1 – Wrong number of duplicates (caught by Alix)

When profiling the dataset in notebook 01, the AI reported 5,269 duplicate rows, whereas checking the data directly showed 5,205 exact duplicates. The AI compared only the 30 input features and ignored the target label, grouping rows that share identical features but have different labels together with true duplicates. Those 64 extra pairs are not exact duplicates, but conflicting feature combinations. We updated the check to evaluate duplicates across the 30 features and the label jointly, separating the 5,205 exact duplicates from the 64 conflicting feature combinations in notebook 01.

Flaw 2 – Test evaluation planned too early (caught by Lou-Ann)

In an early step plan, the AI placed evaluation on the test set before the ensemble models and the out-of-course model were tested. Evaluating on the test set at that point would expose test performance before final model selection is complete, risking bias if any later model choice or adjustment is influenced by those results. The AI relied on a generic sequence of steps rather than enforcing strict isolation of the holdout set until model selection is finished. We changed the workflow so all model comparisons happen with cross-validation first, keeping test.csv for a single evaluation once all models are compared, with notebook 06 as the only notebook loading test.csv.

Flaw 3 – Wrong majority-class baseline (caught by Alix)

The AI stated that a majority-class baseline would always predict the legitimate class and reach roughly 56% accuracy. That reflected the raw dataset prior to deduplication, whereas removing duplicates shifts the distribution so phishing becomes the majority class at 51.6%. Using the pre-deduplication class balance gave an inaccurate baseline expectation. We recomputed the class balance on the deduplicated data and updated notebook 02 so the baseline always predicts phishing, giving a recall of 1.0 and a precision of 0.516.

Flaw 4 – Optimistic score for the neural network (caught by Lou-Ann)

In notebook 05, the AI tuned the MLP hyperparameters with a grid search on the training set and then measured its score using cross-validation on that same training set. Because the same data was used to choose the hyperparameters and evaluate performance, the score has a slight optimistic bias. We replaced this with nested cross-validation so grid search runs inside each inner loop and each outer validation fold stays separate from hyperparameter selection. The nested ROC-AUC is 0.980 ± 0.005 compared to 0.982 without nesting, a small difference that keeps the conclusion unchanged: the MLP remains well below Gradient Boosting (0.993).

Flaw 5 – Wrong encoding assumption (caught by Alix)

The AI assumed that all features follow the same encoding described in the dataset documentation, with -1 indicating phishing, 0 suspicious, and 1 legitimate. Checking the correlation of each feature with the target showed that 10 features are positively correlated with phishing, meaning their sign behaves in the opposite direction to that uniform rule. Relying on the documentation without checking empirical alignment against the target can lead to misreading feature behavior. We added a check on correlation signs before interpreting features, listed these 10 features in section 6 of notebook 01, and noted this point as a limitation in the report.

Flaw 6 – L1 stability not informative (caught by Lou-Ann)

In notebook 04, the AI evaluated L1 feature selection stability across bootstrap samples using C = 0.03, which resulted in 12 features being selected in 100% of samples. With C = 0.03, stability did not differentiate among those features enough to provide a clear ranking. We tested smaller values of C and chose C = 0.005, where only 3 features (AnchorURL, HTTPS, and ServerFormHandler) are always selected and 6 others appear in some samples, giving a clearer ranking that aligns with the other selection methods.

Flaw 7 – Test set evaluated before the final model was chosen (caught by Alix)

During final evaluation, the AI started running test-set evaluation in notebook 06 while work in notebook 05 was not yet finished. Choosing or finalizing a model after seeing test results would introduce bias into model selection. The AI followed a step order without verifying that model comparison was complete. We ran notebook 05 first to compare all models with repeated cross-validation and select Gradient Boosting, and only then ran notebook 06 on the test set.

Flaw 8 – Wrong statement about scikit-learn (caught by Alix)

The AI stated that penalty="l1" no longer works in recent versions of scikit-learn. That confuses deprecation with removal: in scikit-learn 1.9.1, penalty="l1" still runs and emits a FutureWarning, as it is deprecated and scheduled for removal in version 1.10, with l1_ratio=1 as the recommended alternative. We corrected the note in notebook 04, updated the code to use l1_ratio=1, and verified that penalty="l1" in scikit-learn 1.9.1 produces a FutureWarning rather than an error.