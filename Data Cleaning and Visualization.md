1. Source of Dataset and Dataset Size

The dataset used in this experiment was collected from multiple reliable cybersecurity sources to ensure diversity and real-world relevance. Verified phishing URLs were obtained from PhishTank and OpenPhish, which provide continuously updated phishing feeds. Legitimate website URLs were collected from publicly available safe browsing sources and Kaggle phishing datasets. Domain-related metadata such as domain age and registrar information were extracted using the WHOIS API.

Python libraries such as requests and BeautifulSoup were used to gather and structure URL-based features. The collected data was stored in CSV format using Pandas.

The final compiled dataset consists of 10,000 URL samples, out of which 5,000 are phishing websites and 5,000 are legitimate websites. The dataset initially contained 18 structured features including URL length, presence of IP address, number of special characters, domain age, HTTPS status, and other security-related attributes.

2. Purpose of Dataset Collection

The dataset was collected to develop a supervised machine learning model capable of classifying websites as phishing or legitimate. Phishing attacks are one of the most common cyber threats and continuously evolve in structure and technique. Traditional rule-based detection systems are often insufficient in detecting newly crafted phishing URLs.

By collecting and preparing this dataset, the objective is to identify meaningful patterns in URL structures and domain properties that distinguish phishing websites from legitimate ones. This dataset enables training a binary classification model that can be integrated into browser extensions, email filters, or real-time monitoring systems to prevent credential theft and financial fraud.

3. Inspection of Raw Data and Data Quality Issues

After loading the dataset into the Python environment using Pandas, an initial inspection was performed using functions such as .head(), .info(), .describe(), and .isnull().sum().

The inspection revealed several data quality issues. Some entries contained missing values, particularly in the domain age column where WHOIS information was unavailable. Duplicate URLs were detected due to multiple sources contributing overlapping entries. Label inconsistencies were observed, where some entries used textual labels such as “Phishing” and “Legitimate” while others used numeric encodings like 0 and 1.

Additionally, extreme values were observed in URL length, with some URLs exceeding normal length limits, indicating potential outliers. Certain numerical columns were stored as object data types due to formatting inconsistencies. In early versions of the raw dataset, class imbalance was also noticed before balancing was applied.

These issues required systematic cleaning before proceeding to model training.

4. Data Cleaning and Transformation Techniques

The first step in cleaning involved removing duplicate URLs to ensure that the model does not learn biased patterns from repeated entries. This was performed using the drop_duplicates() function in Pandas.

Missing values in the domain age column were handled using median imputation to avoid distortion from extreme values. For categorical inconsistencies, label encoding was standardized such that phishing websites were assigned the value 1 and legitimate websites were assigned 0.

Structural errors were corrected by converting numerical columns stored as strings into appropriate numeric formats. Outliers in URL length were handled using the Interquartile Range (IQR) method. URLs that significantly exceeded normal distribution ranges were removed to prevent skewing of model training.

After cleaning, numerical features were scaled using StandardScaler from Scikit-learn. Scaling ensures that features such as URL length and domain age operate on comparable scales, improving model convergence and performance.

5. Feature Engineering and Selection Methodology

Feature engineering was performed to extract meaningful attributes from the raw URL strings. New features were created such as URL length, count of special characters (such as @, -, %, _), number of subdomains, presence of IP address in URL, HTTPS usage status, and presence of suspicious keywords like “login,” “verify,” and “update.”

These engineered features provide additional insight into phishing behavior patterns, as phishing URLs often use longer structures, suspicious tokens, and newly registered domains.

Feature selection was performed using multiple statistical and model-based techniques. A correlation matrix was generated to identify redundant highly correlated features. Random Forest feature importance was used to determine which variables contributed most significantly to classification. Recursive Feature Elimination (RFE) was also applied to systematically remove less important features.

Based on these techniques, the most influential features included URL length, domain age, HTTPS presence, special character count, and number of subdomains.

6. Data Reduction Methodology

To improve computational efficiency and remove redundancy, dimensionality reduction was applied using Principal Component Analysis (PCA). PCA transformed the original 18 features into 10 principal components while preserving approximately 95% of the dataset’s variance.

Highly correlated features with correlation values greater than 0.85 were removed to reduce multicollinearity. In earlier preprocessing stages, Synthetic Minority Oversampling Technique (SMOTE) was used to ensure balanced representation between phishing and legitimate samples where imbalance was observed.

This reduction process improved training speed and reduced overfitting risk without sacrificing predictive power.

7. Implementation of Cleaning and Visualization

The cleaned dataset was analyzed using visualization techniques to better understand the distribution and relationships between features.

Univariate analysis was performed using histograms and count plots. The class distribution visualization confirmed a balanced dataset of phishing and legitimate URLs. The histogram of URL length revealed that phishing URLs generally tend to be longer compared to legitimate URLs.

Bivariate analysis was conducted using boxplots to compare domain age across classes. It was observed that phishing domains typically have significantly lower domain age, confirming the hypothesis that attackers frequently use newly registered domains.

Multivariate analysis was performed using a correlation heatmap. The heatmap showed a positive correlation between URL length and phishing label, while domain age exhibited a negative correlation with phishing classification. These visual insights validated the importance of selected features.

The dataset after preprocessing contained 10,000 balanced samples with 15 optimized features ready for model training.

   Results

The dataset was successfully cleaned, transformed, and standardized. Missing values were handled appropriately, duplicates were removed, structural inconsistencies were corrected, and outliers were treated. Feature engineering improved dataset richness, while feature selection and PCA reduced redundancy.

Visualization confirmed meaningful patterns that align with known phishing behaviors. The final dataset is fully normalized and ready for supervised machine learning classification.
