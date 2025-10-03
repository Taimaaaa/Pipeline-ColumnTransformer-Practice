# Pipelines & ColumnTransformer – Cereal Dataset
This project demonstrates how to preprocess data before building a machine learning model using scikit-learn Pipelines and ColumnTransformer. The task involves predicting the rating of cereals based on nutritional and categorical features.

## **Project Objectives**

1. Explore and clean the Cereal dataset.
2. Define features (X) and target (y).
3. Split the dataset into training and test sets.
4. Identify feature types: numeric, ordinal, categorical.
5. Build separate preprocessing pipelines for each type:
    * Numeric: imputation (mean) + scaling
    * Categorical: imputation (constant) + one-hot encoding
    * Ordinal (shelf): imputation (most_frequent) + ordinal encoding + scaling

6. Combine the pipelines with a ColumnTransformer.

7. Transform the data into a machine-learning-ready format.

## **Workflow**
1. Dataset

      * Source: Cereal dataset (cereal-kaggle-crawford-modified).
      * Target variable: rating.
      * Features: manufacturer (mfr), type (hot/cold), calories, protein, fat, fiber, sugars, shelf, weight, and others.

2. Preprocessing Steps

    * Numeric pipeline → SimpleImputer(strategy="mean") → StandardScaler()
    * Categorical pipeline → SimpleImputer(strategy="constant", fill_value="MISSING") → OneHotEncoder(handle_unknown="ignore", sparse_output=False)
    * Ordinal pipeline (shelf: bottom → middle → top) → SimpleImputer(strategy="most_frequent") → OrdinalEncoder() → StandardScaler()

3. ColumnTransformer

All three pipelines were combined:

    col_transformer = ColumnTransformer(
    [num_tuple, ord_tuple, ohe_tuple],
    verbose_feature_names_out=False)


  * Fitted only on training data to avoid data leakage.

  * Applied to both train and test sets to produce clean, transformed datasets.
## **Results**

  * Training data transformed: ✔️

  * Test data transformed: ✔️

  * Both outputs now contain imputed, encoded, and scaled features ready for ML modeling.

## **Interpretation**

  * Using ColumnTransformer ensures consistent preprocessing across train/test splits.
  * Missing values are handled automatically with imputation strategies.
  * Categorical and ordinal features are properly encoded into numeric form.
  * Scaling provides standardized feature ranges for improved model performance.

## **Key Takeaway**

The use of pipelines + column transformers allows for a modular and reproducible ML workflow. This ensures preprocessing is applied consistently and efficiently, making the dataset fully ready for machine learning models.
