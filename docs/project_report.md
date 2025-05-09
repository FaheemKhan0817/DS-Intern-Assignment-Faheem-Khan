# Smart Factory Energy Prediction Challenge: Project Report

## 1. Approach to the Problem

### Data Preprocessing
1. **Data Cleaning**:
   - Addressed 23,465 missing values using time-based interpolation and median imputation.
   - Replaced 314 negative energy consumption values with the median of valid values.
   - Capped extreme outliers (>5 standard deviations) for numerical features, including `lighting_energy` and `zone1_temperature`.

2. **Feature Engineering**:
   - Added time-based features (`hour`, `day`, `month`) and their cyclical encodings.
   - Created lag features (`energy_lag_1h`, `energy_lag_2h`, etc.) and rolling statistics (`energy_rolling_mean_3h`, etc.).
   - Derived zone heat indices and aggregated zone temperature and humidity metrics.

3. **Multicollinearity Reduction**:
   - Conducted Variance Inflation Factor (VIF) analysis to reduce multicollinearity.
   - Features reduced from 107 to 30 by removing redundant and highly correlated variables.

### Model Development
1. **Algorithm Comparison**:
   - Trained and evaluated three models: ElasticNet, LightGBM, and XGBoost.
   - Performed feature selection using Lasso regression to retain the top 15 features.
2. **Evaluation Metrics**:
   - R² (coefficient of determination)
   - RMSE (Root Mean Squared Error)
   - MAE (Mean Absolute Error)

---

## 2. Key Insights from the Data

### Feature Importance
- **Top Features**:
  - `energy_rolling_mean_3h`: 52.75% importance
  - `energy_lag_2h`: 23.62% importance
  - `energy_lag_1h`: 23.45% importance
- Zone temperatures and heat indices contributed minimally but provided additional context.

### Data Patterns
1. Short-term energy lags (1-3 hours) are the strongest predictors of current energy consumption.
2. Zone-specific features like temperature and humidity influence energy usage but are less significant than historical energy patterns.
3. Random variables (`random_variable1`, `random_variable2`) had negligible correlation with the target and were excluded from modeling.

---

## 3. Model Performance Evaluation

### Model Comparison
| Model        | R²     | RMSE   | MAE   |
|--------------|---------|--------|-------|
| **ElasticNet** | **0.9985** | **5.11** | **2.12** |
| LightGBM     | 0.9711 | 22.54  | 12.02 |
| XGBoost      | 0.9427 | 31.71  | 13.44 |

### Best Model: ElasticNet
- Achieved R² = 0.9985, RMSE = 5.11, and MAE = 2.12.
- Selected 15 features for prediction:
  - Energy lags (`energy_lag_1h`, `energy_lag_2h`)
  - Rolling mean (`energy_rolling_mean_3h`)
  - Zone temperatures (`zone1_temperature`, `zone2_temperature`, etc.)
  - Zone heat indices (`zone1_heat_index`, `zone2_heat_index`, etc.)

---

## 4. Recommendations for Reducing Equipment Energy Consumption

### 1. Leverage Short-Term Energy Patterns
- Use recent energy consumption (1-3 hours) to predict and manage energy usage efficiently.
- Implement predictive control strategies to adjust energy usage dynamically.

### 2. Optimize Zone Temperatures
- Focus on optimizing temperature setpoints in high-impact zones (e.g., Zone 1, Zone 2).
- Monitor temperature-humidity interactions (heat indices) for energy-efficient HVAC operation.

### 3. Deploy Predictive Maintenance
- Use the model to detect anomalies in energy consumption patterns.
- Schedule preventive maintenance for equipment showing abnormal energy usage.

### 4. Real-Time Monitoring and Alerts
- Deploy a dashboard to visualize energy predictions and identify inefficiencies.
- Implement automated alerts for unusual consumption patterns to enable quick interventions.

---

## 5. Future Work
1. **Incorporate Production Schedules**:
   - Integrate production data to normalize energy predictions based on factory operations.
2. **Zone-Specific Models**:
   - Develop sub-models for each zone to provide granular insights and recommendations.
3. **External Factor Integration**:
   - Include weather forecasts and energy pricing data to enhance prediction accuracy.

---

## 6. Conclusion
The ElasticNet model demonstrated exceptional accuracy (R² = 0.9985) in predicting energy consumption, leveraging historical energy patterns and zone-specific features. By implementing the recommendations outlined above, the manufacturing facility can achieve significant energy savings and operational efficiencies.