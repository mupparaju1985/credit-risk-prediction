##Optimizing Credit Portfolio Risk: A Machine Learning Approach to Predicting Loan Default

Table of Contents
1. Business Problem	1
2. Background and History	1
3. Data Explanation	2
4. Methods	3
5. Analysis	3
6. Conclusion	5
7. Assumptions	5
8. Limitations	5
9. Challenges	6
10. Future Uses and Additional Applications	6
11. Recommendations	6
12. Implementation Plan	7
13. Ethical Assessment	7
Appendix: Supporting Documentation	8
A. 10 Questions for the Audience (To be answered in Milestone 3)	8
B. Visualizations	9
References	11



1. Business Problem
Financial institutions face substantial, direct economic losses when borrowers fail to repay their loans. Historically, risk assessment has relied on static credit scoring models that often lead to an overly cautious or reactive approach, forcing banks to either reject creditworthy applicants or unknowingly approve high-risk applicants. The core business problem this project addresses is the transition from reactive loss absorption to proactive risk management. By accurately predicting the probability of default before a loan is finalized, the institution can optimize its entire lending portfolio, significantly reduce non-performing assets (NPAs), and ensure that lending decisions are both profitable and fair to consumers.
2. Background and History
The evaluation of credit risk has traditionally been dominated by scoring systems, such as FICO, which rely heavily on historical payment behavior to generate a single aggregate risk metric. While these methods are robust and regulated, they often fail to capture the complex, non-linear relationships and intricate data patterns that determine a borrower’s future probability of default in a changing economy. The adoption of advanced machine learning is crucial because it enables institutions to dynamically weigh dozens of factors simultaneously, rather than relying on a static scorecard. This project provides a transparent methodology for integrating a predictive model into the credit approval workflow, a necessity for competing in today’s rapidly evolving, data-driven financial landscape.
3. Data Explanation
This analysis is based on the Credit Risk Dataset (Lao Tse, 2020), an open-source collection of historical loan records that serves as a representative proxy for real-world borrower behavior. The dataset contains approximately 32,581 unique records featuring twelve key attributes, including the borrower’s age, annual income, home ownership status, the amount and purpose of the loan, and the length of their credit history.
To ensure the model’s stability and integrity, the raw data underwent rigorous preprocessing. Initial inspection revealed missing values, particularly in the employment length and interest rate fields. These were addressed using median imputation, a statistical technique that preserves the overall distribution of the features without introducing the bias associated with mean imputation. Furthermore, a critical step involves detecting and capping outliers in high-magnitude fields, such as annual income, to prevent extreme values from skewing the model training. Finally, all non-numeric categorical features, such as home ownership and loan intent, were converted into numerical representations using One-Hot Encoding to be processed effectively by the machine learning algorithms.
4. Methods
The project employed a comparative modeling approach, dividing the preprocessed data into training and test sets at a 70:30 ratio to ensure the final evaluation was performed on unseen data. A primary challenge in this analysis was Class Imbalance, as the number of non-defaulting loans far outnumbered the defaults. Training a model directly on this data would yield high apparent accuracy but poor performance at identifying the actual high-risk loans. To correct this, the Synthetic Minority Oversampling Technique (SMOTE) was applied solely to the training subset. This technique generates synthetic examples of the minority class (defaulters), thereby achieving a balanced training environment without fabricating new information in the crucial test data.
Two distinct supervised learning models were selected for comparison, aiming to strike a balance between predictive power and interpretability. Logistic Regression served as a transparent baseline; given its linear nature, the weights assigned to each feature are easily explained to regulators. The XGBoost Classifier, an advanced gradient-boosting framework, was selected for its proven ability to handle complex, non-linear financial data and to maximize predictive performance.
5. Analysis
The models were evaluated based on Recall, which measures the proportion of actual defaulters correctly identified, and the F1-Score, which balances precision and recall. These metrics were prioritized over simple accuracy because the cost of missing a defaulter is significantly higher than the cost of reviewing a safe application.
The XGBoost Classifier demonstrated a far superior balance of performance compared to the baseline. The model achieved a remarkable accuracy of 93.55% and a strong F1-score of 83.44%. Although the recall was recorded at 74.28%, this trade-off is justifiable given the model’s high precision. This performance indicates that the model is significantly more precise than traditional methods, ensuring that while the bank catches the worst loans, it does not alienate creditworthy customers.
An analysis of the Confusion Matrix provides specific operational insights. Out of the total testing pool, the model correctly identified 1,580 defaulters (True Positives) while missing 547 (False Negatives). Crucially, the model incorrectly flagged only 80 safe customers as risky (False Positives). This extremely low false-positive rate validates XGBoost as the operationally superior model for a modern bank that values both risk protection and customer acquisition.
Furthermore, Feature Importance analysis revealed the primary drivers of default. The single most predictive feature was the status of renting a home (person_home_ownership_RENT), suggesting that applicants who rent rather than own are statistically more likely to default. This was followed by the institution's loan grades (specifically, Grades D and C) and the loan-to-income ratio. This confirms that the model is learning from rational financial indicators: borrowers who do not own assets and borrow a large share of their income are correctly flagged as higher risk.
6. Conclusion
The implementation of the XGBoost model effectively addresses the core business problem of proactive risk management. By accurately identifying high-risk applicants with an over 93% accuracy, the model provides financial decision-makers with a powerful tool to protect capital. While the model misses approximately 25% of defaulters, its exceptional precision ensures that the bank does not lose revenue by rejecting good customers.
7. Assumptions
The modeling process rests on several key assumptions. The first is data representativeness, which assumes that historical data accurately reflect the current applicant pool. The second is that the underlying economic environment remains relatively stable; for example, the model assumes that a sudden housing market crash will not invert the relationship between renting and defaulting. Finally, it is assumed that the bank can define a fixed cost for a default, which is necessary to translate the model’s predictive performance into tangible dollar savings.
8. Limitations
A significant technical limitation is the reliance on historical data, which cannot account for sudden macroeconomic shocks, such as recessions, that may dramatically alter default rates outside the trained distribution. Additionally, the "Black Box" nature of the XGBoost algorithm limits interpretability. Unlike Logistic Regression, XGBoost does not provide a simple linear equation for its decisions, which may require the adoption of secondary explainability tools, such as SHAP values, to fully satisfy regulatory inquiries.
9. Challenges
The primary practical challenge encountered was the inherent class imbalance in credit data. Even with SMOTE oversampling, the model must constantly balance the trade-off between catching every fraudster (high Recall) and approving every good customer (high Precision). Another challenge involves data quality dependency; the model is susceptible to missing or erroneous data. If the data pipeline fails to capture fields like employment length correctly, the accuracy of predictions may degrade significantly in a production environment.
10. Future Uses and Additional Applications
The predictive model can be extended beyond simple acceptance or rejection. The output probability can be utilized for dynamic, risk-based pricing, where applicants with an intermediate default probability are offered the loan but at a higher, risk-adjusted interest rate. Furthermore, the model can be applied to portfolio management by identifying existing low-performing loans that may require early intervention or restructuring before they become non-performing assets.
11. Recommendations
It is recommended that the institution immediately proceed to a controlled pilot phase using the XGBoost model. Specifically, the bank should implement a threshold adjustment strategy. A lower probability threshold could be used to catch more defaulters, though this must be balanced against the risk of rejecting good customers. Additionally, a "Human-in-the-Loop" system is recommended for borderline cases, where the model automatically approves low-risk loans and rejects high-risk ones, but refers medium-risk applications to human underwriters for manual review.
12. Implementation Plan
The implementation plan should be executed in phased stages. The first phase involves a "Shadow Deployment" lasting 4 to 6 weeks, during which the model runs in parallel with the current loan approval system. During this time, model recommendations are recorded but not acted on, allowing lending officers to verify them against their own decisions. Following a successful audit, the second phase would involve live integration via an API into the automated loan origination system. The model's prediction would then become the primary risk score, triggering automatic approval, rejection, or manual review based on predefined risk thresholds.
13. Ethical Assessment
The adoption of a predictive credit model necessitates a robust ethical assessment. The primary concern is Algorithmic Bias, specifically the risk that the model inadvertently discriminates against protected groups. The finding that renting is the top predictor of default must be scrutinized, as home ownership rates often correlate with race and socioeconomic status. To ensure compliance with the Fair Credit Reporting Act (FCRA), the implementation must ensure that every rejected applicant receives an apparent, concise, and understandable Reason for Adverse Action. The transparency provided by the feature importance analysis is the essential technical tool for meeting this legal and ethical requirement, ensuring that the model remains accountable and fair.
 
Appendix: Supporting Documentation
A. 10 Questions for the Audience (To be answered in Milestone 3)
These are questions anticipated from stakeholders, executives, and regulators during the final presentation.
1. How will this model perform if the economy enters a recession next year? 
Answer: The model may drift during economic shifts. We will implement quarterly retraining and a "concept drift" monitor. If the economic baseline shifts, the model will be retrained on the most recent 6 months of data.
2. Since renting is a top risk factor, how do we ensure we are not unfairly discriminating against lower-income applicants? 
Answer: We will perform a Disparate Impact Analysis. If "Renting" is found to be a proxy for race rather than financial stability in our specific region, we will reduce its weight to comply with Fair Lending laws.
3. What is the estimated annual dollar amount that this model will save the bank? 
Answer: The model correctly identified 1,580 defaulters in the test set. If the average loan loss is $10,000, identifying these loans could avoid over $15 million in losses in this dataset alone.
4. The model wrongly rejects 80 good customers; how do we handle their complaints? 
Answer: We will implement a manual appeal process. Any customer rejected solely on the basis of the model score can request a human review, during which an underwriter can override the decision with supplementary evidence.
5. How frequently does this model need to be retrained? 
Answer: We recommend retraining quarterly. It can be managed by the existing IT team using an automated pipeline that triggers alerts only if accuracy drops below 90%.
6. Can this "Black Box" XGBoost model explain precisely why it rejected a specific person? 
Answer: Yes, we utilize SHAP (Shapley Additive exPlanations) values. This tool breaks down every prediction to show precisely how much each feature contributed, allowing us to generate legal reason codes.
7. What happens if the credit bureau data feed goes down? 
Answer: We have designed a fallback system. If data is missing, the application is routed to a simpler Logistic Regression model using fewer features or sent directly to a human underwriter.
8. Can we adjust the risk sensitivity without retraining? 
Answer: Yes, we can adjust the "Probability Threshold." Lowering it from 0.5 to 0.3 makes the model stricter; raising it to 0.7 makes it more lenient.
9. Why did you choose XGBoost over Logistic Regression? 
Answer: XGBoost offered 93% accuracy compared to ~84% for Logistic Regression. It better captures complex, non-linear financial behaviors necessary for high-precision risk management.
10. What is the cost to integrate this into legacy systems? 
 We estimate a 12-week timeline using a microservices architecture (Docker/REST API) to encapsulate the Python model, enabling it to communicate with legacy systems with minimal infrastructure changes.

B. Visualizations
•	Figure 1: Impact of Loan-to-Income Ratio on Default Status.
 
•	Figure 2: XGBoost Confusion Matrix.
 
•	Figure 3: Top 5 Predictors of Loan Default.
 
 
References
Davydenko, S. A., Strebulaev, I. A., & Zhao, Y. (2015). A market-based study of the cost of default. The Review of Financial Studies, 28(1), 1–45.
Lao Tse. (2020). Credit Risk Dataset (Version 1) [Data set]. Kaggle. https://www.kaggle.com/datasets/laotse/credit-risk-dataset
US Congress. (1970). Fair Credit Reporting Act. 15 U.S.C. § 1681 et seq.
<img width="468" height="636" alt="image" src="https://github.com/user-attachments/assets/255f0c43-173d-4d00-9592-dcef98c77634" />
