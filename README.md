Student-Academic-Engagement-Using-Library-Dataset
This project analyzes student academic engagement by combining academic records with library usage data, and applies multiple machine learning and data mining algorithms (Random Forest, J48, k-means, Hierarchical clustering, Apriori, FP-Growth) using Weka.​

Project Objectives Measure academic engagement using both:

Academic attributes (CGPA, attendance, performance index, risk level).

Library attributes (days issued, renewals, fines, late returns, visit-based features where available).​​

Predict academic performance / engagement level using supervised models.

Discover natural engagement groups using clustering.

Extract association rules that link scholarship, hostel/day-scholar, book categories and performance.

Dataset The final dataset (approx. 200 rows, 30+ attributes) contains:

Student attributes: Student_ID, Gender, Age, Department, Year_of_Study, Section, CGPA, Attendance_Percentage, Scholarship_Status, Hostel_DayScholar, Performance_Index, Scholarship_Flag, Student_Category, Risk_Level, CGPA_Category​

Library usage attributes: Book_Category, Number_of_Days_Issued, Renew_Count, Fine_Amount, Late_Return_Count (plus optional: Library_Visit_Frequency, Total_Library_Visits, Reading_Duration_Hours, if present).​​

Target variables:

Academic_Performance ∈ {Excellent, Good, Average, Poor}.

Derived binary label Engagement_Level ∈ {High, Low} (High = Excellent/Good, Low = Average/Poor) for higher-accuracy Random Forest experiments.

Non-predictive identifiers (e.g., Student_Name, Book_Title, Author_Name, Publisher, ISBN, Issue_Date, Due_Date, Return_Date) are removed from most models to reduce noise.​

Methods Classification (Supervised Learning) Random Forest (Weka)

Input: student + library engagement attributes.

Target: Academic_Performance (4 classes) and Engagement_Level (binary).

Achieved about 72% accuracy and kappa ≈ 0.61 on the 4-class problem using 10-fold cross-validation on 200 instances, with high AUC (~0.93).​​

Best at identifying Good and Poor students, useful for flagging at-risk cases.

J48 Decision Tree (Weka)

Used as an interpretable baseline to compare with Random Forest.

Helps visualize decision rules based on CGPA, attendance and library usage.​

Clustering (Unsupervised Learning) k-means (k = 3)

Attributes: numeric engagement features (CGPA, attendance, performance index, days issued, renewals, fines, late returns, etc.).​

Output: three clusters interpreted as High, Medium and Low engagement groups.

Hierarchical Clustering

Same feature set as k-means.

Dendrogram used to visually inspect how engagement groups form step-by-step.

Association Rule Mining Apriori

FP-Growth

Both applied on a categorical / discretized version of the dataset:

Discretized CGPA, Attendance_Percentage, Number_of_Days_Issued, Renew_Count, Fine_Amount, Late_Return_Count into ranges.

Used attributes such as Scholarship_Status, Hostel_DayScholar, Book_Category, Language, Risk_Level, Academic_Performance.

Found strong rules, for example:

Hostel + Scholarship + non-Civil book categories → specific performance patterns.

Consistent relationships between scholarship flags and academic outcomes.

Tools and Environment Language / Platform: Weka 3.x GUI (Explorer).

Algorithms: RandomForest, J48, SimpleKMeans, HierarchicalClusterer, Apriori, FPGrowth.

Data format: CSV and ARFF files (200 instances, 20–30 attributes depending on the experiment).​​

Repository Structure (suggested) data/

students_raw.csv – original dataset.

students_200x20_raw.csv – selected 20-column version.

students_engagement_rf.csv – binary engagement dataset for high-accuracy Random Forest.

students_fp_growth.arff – discretized categorical dataset for Apriori/FP-Growth.

notebooks/ or weka_configs/

Notes on filters and parameter settings.

results/

Screenshots or text exports of Weka outputs (Random Forest, k-means, Apriori, FP-Growth).

README.md (this file)

How to Reproduce Open the dataset in Weka (Preprocess).

For classification:

Set class = Academic_Performance or Engagement_Level.

Choose RandomForest or J48 in the Classify tab.

Use 10-fold cross-validation and record accuracy, kappa and confusion matrix.

For clustering:

Remove ID and non-numeric fields.

Run SimpleKMeans (k = 3) and HierarchicalClusterer on engagement features.

For association rules:

Apply Discretize filter to numeric attributes.

Run Apriori or FPGrowth in the Associate tab to generate rules.

Conclusion This project shows that:

Random Forest is an effective model for predicting student academic performance / engagement using combined academic and library data.

k-means and Hierarchical clustering reveal natural engagement groups based on usage behaviour.

Apriori and FP-Growth uncover interpretable patterns linking scholarship, hostel status, book categories and engagement, which can support targeted academic interventions.

You can adapt this template by adding your screenshots, exact accuracy numbers, and links to your Weka outputs.
