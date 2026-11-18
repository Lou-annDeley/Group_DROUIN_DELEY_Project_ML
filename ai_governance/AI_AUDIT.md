AI Audit

Flaw 1 – Wrong number of duplicates (Alix)
AI output: "5,269 duplicate rows".
Problem: the real number of exact duplicates is 5,205.
Root cause: the AI compared the features only and ignored the label.
Fix: count duplicates on features + label.
Check: notebook 01 shows 5,205 exact duplicates and 64 conflicting combinations.

Flaw 2 – Wrong majority-class baseline (Alix)
AI output: "the majority baseline always predicts legitimate, about 56% accuracy".
Problem: after deduplication, phishing is the majority class (51.6%).
Root cause: the AI used the class balance before removing duplicates.
Fix: compute the class balance after deduplication.
Check: notebook 02 shows the baseline predicts phishing (recall = 1.0, precision = 0.516).

Flaw 3 – Wrong encoding assumption (Alix)
AI output: "features are ordered: phishing < suspicious < legitimate".
Problem: 10 features are positively correlated with phishing, so the encoding is not the same for all features.
Root cause: the AI trusted the dataset description without checking the data.
Fix: check the sign of the correlation of each feature with the target.
Check: notebook 01, section 6 lists these 10 features. Noted as a limitation in the report.
