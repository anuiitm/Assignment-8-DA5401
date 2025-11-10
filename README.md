# Assignment-8-DA5401 - Bike Sharing Demand Prediction: An Ensemble Learning Approach
## NAME - Anubhav agarwal
## Roll No - HS22H059
## Documentation
### The repo contains a .ipynb file and README.md file, the main submission is in .ipynb file. Please use that to see my work

## Dataset

**Bike Sharing Demand Dataset (Hourly Data)**
*   **Citation**: Fanaee-T, Hadi, and Gamper, H. (2014). Bikeshare Data Set. UCI Machine Learning Repository.
*   **Source**: UCI Machine Learning Repository - Bike Sharing Dataset

## Tasks Performed

### Part A: Data Preprocessing and Baseline

1.  **Data Loading and Feature Engineering**: Loaded the `hour.csv` file, dropped irrelevant columns (`instant`, `dteday`, `casual`, `registered`), and converted categorical features (`season`, `yr`, `mnth`, `hr`, `weekday`, `weathersit`, `holiday`) into a numerical format using One-Hot Encoding.
2.  **Train/Test Split**: Split the preprocessed data into training (80%) and testing (20%) sets.
3.  **Baseline Model Training and Evaluation**: Trained a single Decision Tree Regressor (max_depth=6) and a Linear Regression model. Evaluated both using RMSE. The Linear Regression model, with a lower RMSE, was chosen as the baseline.

### Part B: Ensemble Techniques for Bias and Variance Reduction

1.  **Bagging (Variance Reduction)**:
    *   **Hypothesis**: Bagging primarily targets variance reduction.
    *   **Implementation**: Implemented a Bagging Regressor using the Decision Tree Regressor (max_depth=6) as the base estimator with 50 estimators.
    *   **Result**: Bagging successfully reduced variance, showing an improved RMSE compared to the single Decision Tree.
2.  **Boosting (Bias Reduction)**:
    *   **Hypothesis**: Boosting primarily targets bias reduction.
    *   **Implementation**: Implemented a Gradient Boosting Regressor (n_estimators=100, learning_rate=0.1, max_depth=3).
    *   **Result**: Gradient Boosting achieved a significantly lower RMSE than both single models and the Bagging ensemble, supporting its role in bias reduction.

### Part C: Stacking for Optimal Performance

1.  **Stacking Implementation**:
    *   **Principle Explained**: Stacking combines diverse base learners and uses a meta-learner to optimally combine their predictions, leveraging the strengths of each model.
    *   **Base Learners (Level-0)**: K-Nearest Neighbors Regressor, Bagging Regressor (from Part B), and Gradient Boosting Regressor (from Part B).
    *   **Meta-Learner (Level-1)**: Ridge Regression model.
    *   **Implementation**: Combined these into a Stacking Regressor.
2.  **Final Evaluation**: Calculated the RMSE for the Stacking Regressor on the test set.

### Part D: Final Analysis

## Comparative Table of Model Performance (RMSE)

| Model                               | RMSE       |
| :---------------------------------- | :--------- |
| Single Decision Tree Regressor      | 118.4555   |
| Linear Regression (Baseline)        | 100.4459   |
| Bagging Regressor                   | 112.3521   |
| Gradient Boosting Regressor         | 78.9652    |
| **Stacking Regressor**              | **67.0291**|

## Conclusion

Based on the Root Mean Squared Error (RMSE) values, the **Stacking Regressor** is the best-performing model, achieving an RMSE of **67.0291**. This significantly outperforms all other models, including the single models and the other ensemble techniques.

### Why Stacking Outperformed the Single Model Baseline:

The Stacking Regressor's superior performance is attributed to its sophisticated approach to ensemble learning, effectively leveraging the principles of the bias-variance trade-off and model diversity:

1.  **Bias-Variance Trade-off**: Stacking intelligently combines models that address different aspects of prediction error. For instance, the Bagging Regressor reduces variance by averaging high-variance Decision Trees, while the Gradient Boosting Regressor focuses on bias reduction by sequentially correcting errors. The Meta-Learner (Ridge Regression) learns to optimally weigh these diverse predictions, finding a sweet spot that minimizes the combined bias and variance more effectively than individual models or simpler ensembles.

2.  **Model Diversity**: The success of Stacking hinges on the diversity of its base learners. By incorporating models with fundamentally different learning paradigms—K-Nearest Neighbors (instance-based), Bagging (tree-based, variance-reducing), and Gradient Boosting (tree-based, bias-reducing)—the Stacking Regressor captures a wider array of patterns and relationships within the data. This diversity ensures that errors made by one base model are not systematically replicated by others, allowing the meta-learner to synthesize varied 'opinions' into a more robust and accurate final prediction.
