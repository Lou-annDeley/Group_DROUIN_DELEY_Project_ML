Prompt 1 (Alix – Notebook 01)

Using relative paths on data/phishing.csv for binary phishing classification, write modular Python code to inspect dataset shape, column types, missing values, class balance, exact duplicates across all 30 features and the label, and rows sharing identical features with conflicting labels. State the statistical assumptions behind non-parametric checks on skewed or discrete web and URL features, define a fallback rule before saving data/phishing_clean.csv, and keep preprocessing and scaling out of this step so nothing is fit before splitting into train and test sets.

Prompt 2 (Lou-Ann – Notebook 02)

Using data/train.csv and data/test.csv with random_state=42 and stratified cross-validation, build a baseline classification pipeline in notebook 02 where preprocessing steps are fit only inside training folds and on the training split, never on test data. Recompute the majority-class baseline on the deduplicated data rather than relying on pre-deduplication counts, report precision, recall, F1, ROC-AUC, and PR-AUC alongside model assumptions, and include a fallback adjustment if regularization or probability calibration needs refinement.

Prompt 3 (Alix – Notebook 04)

In notebook 04, working strictly on the training data with stratified cross-validation and random_state=42, compare filter, wrapper, L1 selection, and permutation importance without touching test.csv. Tune regularization strength (such as C = 0.005 vs. C = 0.03) so L1 bootstrap stability gives a clear ranking rather than saturating at 100% across too many features, note caveats of permutation importance when features are correlated, define a fallback rule for keeping a reduced feature subset, and verify scikit-learn parameter deprecation behavior (FutureWarning vs. error, using l1_ratio=1).

Prompt 4 (Lou-Ann – Notebooks 05 and 06)

In notebooks 05 and 06, compare ensemble models and an MLP classifier using fixed random_state=42 and strict isolation of test.csv. Use nested cross-validation when tuning MLP hyperparameters so inner search never touches outer validation folds, compare against non-nested tuning and ensemble models, and reserve test.csv for a single evaluation in notebook 06 only after notebook 05 finishes model comparison and selects the final model. Include uncertainty estimates, error and failure mode analysis, and a fallback to a well-regularized ensemble if the MLP overfits or lacks stability.

Note: the prompts are the improved versions we wrote after auditing the AI's outputs (see AI_AUDIT.md). Our original prompts were much shorter and less constrained, which caused the flaws listed in the audit.