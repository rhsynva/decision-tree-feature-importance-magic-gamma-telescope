Magic Gamma Telescope Classification Dataset: Decision Tree and Feature Importance Analysis
This project focuses on the classification of high-energy gamma particles using the MAGIC Gamma Telescope dataset through a Decision Tree approach. The analysis includes model optimization, bias correction using class weights, and identifying the most influential features in the decision-making process. The goal is to simulate the registration of high-energy gamma particles in a ground-based atmospheric Cherenkov telescope. The classification distinguishes between Gamma rays (signal) and Hadron showers (background). Decision Trees were selected for this task due to their flowchart-like logic, which closely mimics human decision-making by splitting data into increasingly "pure" groups based on specific criteria. The project was developed using Python in a Jupyter Notebook environment. I utilized Pandas and NumPy for data manipulation, and Matplotlib and Seaborn for advanced visualization. The machine learning implementation relied on Scikit-learn, specifically using DecisionTreeClassifier, GridSearchCV, and tree visualization tools.

Workflow and Methodology:
1. Data Preprocessing
To ensure the model receives clean data, several steps were performed. Redundant columns were dropped using the drop function to reduce dimensionality. For outlier detection and removal, I utilized Boxplots and Histograms to identify columns with a high probability of outliers. Based on the Boxplot analysis, these outliers were removed. In the visual representation, the empty circles represent outliers while the whiskers represent the borders. Any resulting empty spaces from the removal were filled with the mean of the respective column to maintain data integrity. Finally, Label Encoding was performed to prepare the target variable.

2. Training and Logic
The dataset was divided into 80% Training and 20% Testing sets. Unlike distance-based algorithms like KNN, scaling is not mandatory or primarily needed for the Decision Tree algorithm, as the model splits data based on feature thresholds rather than calculating distances.

3.Hyperparameter Tuning and Decision Tree Execution
I implemented Grid Search to determine the best parameters for the model. After completing the Grid Search, the Decision Tree was executed. The final classification model was trained on the data, and a Classification Report was generated for the final analysis.

4.Model Evaluation and Bias Management
Confusion Matrix Analysis
To evaluate the model, I generated a heatmap of the confusion matrix. The analysis showed 2,300 True Negatives (Class 0 correctly predicted) and 710 True Positives (Class 1 correctly predicted). There were 180 False Positives, representing a relatively low error rate for Class 0. However, with 350 False Negatives, the model was more likely to miss a Class 1 case by mistakenly labeling it as 0.
<img width="662" height="521" alt="HeatMap 1" src="https://github.com/user-attachments/assets/9780e254-c6c5-473f-b700-314b0f153990" />

5.Visualizing the Decision Logic
To see how the model reached its conclusions, I used the plot_tree function with a large figure size to render the entire flowchart. This visualization shows every decision node, the feature used for the split, and the resulting entropy or Gini impurity at each stage.

6.Addressing Data Imbalance
Since the model initially saw more Class 0 data, it showed a bias toward that class. To correct this, I re-trained the model using the class_weight="balanced" parameter. This forced the model to pay more attention to Class 1. While the overall accuracy dropped by approximately 1%, the balance of the model improved significantly, ensuring it was no longer heavily biased toward a single side. <img width="655" height="521" alt="image" src="https://github.com/user-attachments/assets/08fb36df-0c3f-4349-b26b-c138fb2d6f89" />


7.Feature Importance and Final Analysis
A key advantage of Decision Trees is the built-in feature_importances_ attribute. This value is calculated based on how much each feature reduces Gini Impurity or Entropy. A feature is considered more important if it appears higher in the tree and successfully splits a larger number of nodes. To visualize this, I created a bar chart showing the impact of each column. The analysis revealed that fAlpha is the most influential feature in determining the particle type, while fM3Trans has the least impact on the model's final decisions. <img width="694" height="571" alt="Bar Chart" src="https://github.com/user-attachments/assets/6457329e-e504-4c78-9680-bc12cc32977a" />
