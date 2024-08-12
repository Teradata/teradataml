## Workflows showcasing capabilities of Teradata Python package for Advanced Analytics.

AutoML, or Automated Machine Learning, represents a method for streamlining the entire process of machine learning 
pipeline in automated way. Teradataml AutoML consists of five different phases covering different processes in 
automated way:
* #### Feature Exploration: It explores available features and provide insights such as column summary, categorical 
  features distinct count, outlier percentage details, futile column details, and target column distribution.
* #### Feature Engineering: It handles data anomalies such as duplicate rows handling, missing value handling, futile 
  column handling. Additionally, it executes various feature transformations based on the data types of the features.
* #### Data Preparation: It performs various steps to prepare the data for model training, including feature selection, 
  feature scaling, and splitting the data into training and validation sets.
* #### Model Training: It performs hyperparameter tuning with available models.
* #### Model Evaluation: It assesses various trained models and generates a model leaderboard that includes performance 
  metrics, detail on the applied feature selection method, and corresponding rankings for each model in ascending order. The model ranked 1 indicates the best-performing model for the given dataset.

For community support, please visit the [Teradata Community](https://support.teradata.com/community?id=community_forum&sys_id=14fe131e1bf7f304682ca8233a4bcb1d).

For Teradata customer support, please visit [Teradata Support](https://support.teradata.com/csm).

Copyright 2024, Teradata. All Rights Reserved.

## Following workflows in the form of Jupyter notebooks are provided for both Auto and Custom run with corresponding jsons:
* #### Auto Run Notebooks
    - ##### Binary_Classification__Bank_Churn_Prediction.ipynb
    - ##### Binary_Classification__Bank_Marketing_Outcome_Prediction.ipynb
    - ##### Binary_Classification__Breast_Cancer_Prediction.ipynb
    - ##### Binary_Classification__Titanic_Survival_Prediction_Deploy_Models.ipynb
    - ##### Binary_Classification__Titanic_Survival_Prediction_Load_Models.ipynb
    - ##### Binary_Classification__Wine_Quality_Prediction.ipynb
    - ##### Multi_Classification__BMI_Value_Prediction_Deploy_Models.ipynb
    - ##### Multi_Classification__BMI_Value_Prediction_Load_Models.ipynb
    - ##### Multi_Classification__Glass_Type_Prediction.ipynb
    - ##### Multi_Classification__Iris_Flower_Type_Prediction.ipynb
    - ##### Regression__Advertisment_Sales_Prediction_Deploy_Models.ipynb
    - ##### Regression__Advertisment_Sales_Prediction_Load_Models.ipynb
    - ##### Regression__Bike_Sharing_Demand_Prediction.ipynb
    - ##### Regression__Fish_Weight_Prediction.ipynb
    - ##### Regression__House_Price_Prediction.ipynb
    - ##### Regression__Insurance_Charges_Prediction.ipynb
    
* #### Custom Run Notebooks with corresponding jsons
    - ##### Binary_Classification__Bank_Churn_Prediction_Deploy_Models.ipynb
    - ##### Binary_Classification__Bank_Churn_Prediction_Load_Models.ipynb
      - Custom json : custom_bank_churn.json
    - ##### Binary_Classification__Bank_Marketing_Outcome_Prediction.ipynb
      - Custom json : custom_bank_marketing.json
    - ##### Binary_Classification__Breast_Cancer_Prediction.ipynb
      - Custom json : custom_breast_cancer.json
    - ##### Binary_Classification__Titanic_Survival_Prediction.ipynb
      - Custom json : custom_titanic.json
    - ##### Binary_Classification__Wine_Quality_Prediction.ipynb
      - Custom json : custom_wine_quality.json
    - ##### Multi_Classification__Iris_Flower_Type_Prediction.ipynb
      - Custom json : custom_iris.json
    - ##### Regression__Fish_Weight_Prediction.ipynb
      - Custom json : custom_fish_weight.json
    - ##### Regression__House_Price_Prediction.ipynb
      - Custom json : custom_housing.json
    - ##### Regression__Insurance_Charges_Prediction.ipynb
      - Custom json : custom_insurance.json

## Documentation

General product information, including installation instructions, is available in the [Teradata Documentation website](https://docs.teradata.com/search/documents?query=package+python+-lake&filters=category~%2522Programming+Reference%2522_%2522User+Guide%2522*prodname~%2522Teradata+Package+for+Python%2522_%2522Teradata+Python+Package%2522&sort=last_update&virtual-field=title_only&content-lang=)

## License

Use of the Teradata Python Package is governed by the *License Agreement for the Teradata Python Package for Advanced Analytics*. 
After installation, the `LICENSE` and `LICENSE-3RD-PARTY` files are located in the `teradataml` directory of the Python installation directory.
