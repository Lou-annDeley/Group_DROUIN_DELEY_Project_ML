AI Audit – Catch & Correct
Flaw 1 – Wrong number of duplicates (caught by Alix)

When we asked the AI to profile the dataset, it reported 5,269 duplicate rows. When we checked this number in our own notebook, we found only 5,205 exact duplicates. The difference comes from the way the AI counted them: it compared the 30 features only and ignored the label, so websites with the same features but different labels were also counted as duplicates. These rows are not true duplicates: they are conflicting examples. We fixed the count by checking duplicates on the features and the label together. Notebook 01 now shows 5,205 exact duplicates and, separately, 64 conflicting feature combinations.

Flaw 2 – Wrong majority-class baseline (caught by Lou-Ann)

The AI stated that the majority-class baseline would always predict “legitimate” and reach about 56% accuracy. This was true for the raw dataset, but not for the data we actually train on. After removing duplicates, phishing becomes the majority class (51.6%). The AI had used the class balance computed before deduplication and did not update it after this preprocessing step. We fixed this by computing the class balance again on the deduplicated data. Notebook 02 confirms that the baseline always predicts phishing, with a recall of 1.0 and a precision of 0.516.

Flaw 3 – Wrong encoding assumption (caught by Alix)

The AI assumed that all features follow the same order, with −1 meaning a phishing sign, 0 suspicious and 1 a legitimate sign, as written in the dataset description. When we checked the correlation of each feature with the target, we found that 10 features are positively correlated with phishing, so for them the encoding works the other way round. The AI had trusted the dataset documentation without checking it against the data. We fixed this by computing the sign of the correlation of each feature with the target before interpreting them. Section 6 of notebook 01 lists these 10 features, and we note this as a limitation in the report.