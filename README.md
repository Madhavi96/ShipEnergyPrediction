# 🚢 Energy Consumption Predictor for Ro-Ro Vessels

##  Overview
This project focuses on developing a Machine Learning model to predict the energy consumption of a Danish Ro-Ro passenger ship. The model leverages historical sensor data recorded between February and April 2010, comprising 246 voyages and over 1.6 million data records. By predicting energy consumption, this research aims to optimize fuel efficiency and reduce environmental impact.

##  Motivation
Maritime transport plays a crucial role in global trade and logistics, but it is also a major contributor to greenhouse gas emissions. Ship operators face increasing fuel costs and stringent environmental regulations. Traditional fuel consumption calculations do not account for dynamic factors like wind speed, ocean currents, and cargo weight variations. Machine learning provides a more adaptive and accurate approach to energy consumption prediction.

##  Data Description
The dataset consists of multiple sensor readings, including:
-  **Doppler speed logs**
-  **Gyrocompasses**
-  **GPS readings**
-  **Fuel flow meters**
-  **Rudder angle sensors**
-  **Wind sensors**
-  **Propeller pitch sensors**

Confusion Matrix

![image](https://github.com/user-attachments/assets/b8a217d5-b90b-40f3-ab8a-2bc5a820ddad)

Traget Variable Distribution
![image](https://github.com/user-attachments/assets/5e12e6a4-3933-4ce5-a254-14abc2d2057b)

Feature Distribution
![image](https://github.com/user-attachments/assets/7db0416b-1015-4dec-a1d9-3c1f7fbb6b86)



##  Methodology
###  1. Data Processing
- ** Feature Selection:** Features were chosen based on correlation with the target variable (energy consumption). Redundant and weakly correlated features were removed to prevent overfitting and improve model performance.
- ** Window Interval Selection:** A one-minute resampling window was chosen based on statistical analysis of time gaps.
- ** Data Preparation:**
  -  Timestamps were converted from Windows File Time format.
  -  Missing timestamps were handled through averaging rather than interpolation.
  -  Longitude and latitude data were cleaned and converted into numerical values.
  -  Energy consumption was computed as:
    ```
    EC = fuelDensity * fuelVolumeFlowRate * 60
    ```
  -  StandardScaler was used to normalize the data.
- ** Feature Engineering:** Additional features were engineered based on domain knowledge, including:
  -  **Heading Stability** (difference between true heading and track degree)
  -  **Rudder Difference** (asymmetric steering efforts)

###  2. Model Training & Evaluation
####  Data Split
- The dataset was split into **80% training** and **20% testing**.

####  Model Selection
Two regression models were used:
1.  **Random Forest Regression** – an ensemble learning method that reduces overfitting and captures complex relationships.
2.  **K-Nearest Neighbors (KNN) Regression** – a distance-based method that predicts values based on past observations.

####  Model Training
- ** 5-fold Cross Validation** was used to ensure generalization.
- ** Hyperparameter tuning** was performed using GridSearchCV to optimize model parameters.
- ** Evaluation Metric:** R-Squared (R²) score.

####  Model Comparison
| Model  |  R-Squared Score |
|--------|----------------|
|  Random Forest Regression | 96% |
|  KNN Regression | 91% |

![image](https://github.com/user-attachments/assets/5682cba0-3551-4ff5-ab69-ffe95fc104be)


![image](https://github.com/user-attachments/assets/c349c147-7968-482e-b905-f3ecc04257a3)

Random Forest Regression performed better due to:
-  Superior handling of non-linear relationships.
-  Robustness against noise and missing data.
-  Feature importance analysis for better interpretability.

###  3. Performance Improvements
-  **Feature engineering** played a key role in improving model accuracy.
-  KNN model performance improved by **2%** after hyperparameter tuning.
-  Random Forest did not show significant improvement post-tuning, indicating it was already well-optimized.

##  Challenges & Solutions
- ** Optimal Window Interval:** Selected via histogram analysis and statistical metrics.
- ** Data Imbalance:** Addressed using time-series cross-validation.
- ** Timestamp Conversion Issues:** Adjusted Windows File Time to align with the dataset timeframe.
- ** Accuracy Optimization:** Iterative feature engineering significantly improved model performance.

##  Future Work
-  Implement deep learning models for enhanced accuracy.
-  Incorporate additional sensor data such as weather and sea state conditions.
-  Explore other regression models to further optimize predictions.

##  References
1.  [StandardScaler - Scikit Learn](https://scikit-learn.org/dev/modules/generated/sklearn.preprocessing.StandardScaler.html)
2.  [GridSearchCV - Scikit Learn](https://scikit-learn.org/dev/modules/generated/sklearn.model_selection.GridSearchCV.html)
3.  [MS Smyril Vessel Information](https://www.marinetraffic.com/en/ais/details/ships/shipid:181927/mmsi:231300000/imo:9275218/vessel:SMYRIL)

---
** Contributors:** Ishara Madhavi

For more details, please check the full project report.

