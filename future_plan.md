# Smart Factory Energy Prediction Challenge

## Project Overview
This project aims to predict energy consumption in a smart factory using machine learning models. The data is collected from sensors across various zones in the factory and includes environmental conditions like temperature, humidity, and energy usage.

The goal is to build a robust prediction model to assist facility managers in optimizing energy consumption and reducing costs.

## Repository Structure
```
DS-INTERN-ASSIGNMENT-FOLDER/
│
├── catboost_info/              # Directory for CatBoost model information and related files
│
├── data/                       # Directory containing raw and processed datasets
│   ├── raw/                    # Raw datasets
│   └── processed/              # Processed datasets ready for modeling
│
├── docs/                       # Directory for documentation, including reports, presentations, and guidelines
│   ├── data_description.md     # Detailed description of the dataset and its features
│   ├── project_report.md       # Final project report including methodology, results, and insights
│   └── presentation.pptx       # Project presentation for stakeholders
│
├── EDA/                        # Directory for Exploratory Data Analysis (EDA) notebooks and scripts
│   ├── data_cleaning.ipynb     # Jupyter Notebook for data cleaning exploration
│   ├── feature_analysis.ipynb  # Jupyter Notebook for feature analysis and visualization
│   └── correlation_analysis.ipynb  # Jupyter Notebook for correlation and multicollinearity analysis
│
├── models/                     # Directory for model artifacts and related files
│   ├── ElasticNet_energy_model.pkl  # A saved Elastic Net model for energy prediction
│   ├── CatBoost_energy_model.pkl    # A saved CatBoost model for energy prediction
│   └── model_summary.csv       # Summary file with metrics for all models
│
├── results/                    # Directory for storing results, such as model evaluation metrics, visualizations, etc.
│   ├── predictions.csv         # Predicted energy consumption values for the test dataset
│   ├── correlation_heatmap.png # Heatmap showing feature correlations
│   ├── feature_importance.png  # Bar plot of feature importance for the best model
│   ├── residuals_plot.png      # Residual plot for ElasticNet predictions
│   └── energy_patterns.png     # Visualization of energy consumption patterns
│
├── advanced_Smart_Factory_Energy_Prediction.ipynb  # Jupyter Notebook for advanced energy prediction analysis
│
├── README.md                   # Project README file with an overview, setup instructions, and other relevant information
│
└── simple_energy_consumption.ipynb  # Jupyter Notebook for a simplified energy consumption analysis
```

## Key Results
- **Best Model**: ElasticNet
- **Final R² Score**: 0.9985 (on test set)
- **RMSE**: 5.11
- **Key Features**: Energy lags (`energy_lag_1h`, `energy_lag_2h`), rolling mean (`energy_rolling_mean_3h`), and zone temperatures

## Dataset
The dataset consists of:
- **Target Variable**: `equipment_energy_consumption` (kWh)
- **Features**: Zone temperatures, humidity, outdoor conditions, time-based features, and derived metrics like energy lags and rolling statistics
- **Size**: 15,878 rows and 29 initial features

## How to Run
1. Install dependencies:
   ```
   pip install -r requirements.txt
   ```

2. Run the advanced analysis:
   ```
   jupyter notebook advanced_Smart_Factory_Energy_Prediction.ipynb
   ```

3. Test the saved model:
   ```
   python src/test_model.py
   ```

4. Review outputs in the `results/` folder.

## Recommendations
1. **Short-Term Energy Management**:
   - Leverage recent energy usage patterns for cost optimization.
2. **Zone-Specific Optimization**:
   - Focus on zones with the highest energy consumption (e.g., Zone 1 and Zone 2).
3. **Predictive Maintenance**:
   - Use the model to monitor anomalies and inefficiencies.
4. **Real-Time Monitoring**:
   - Deploy a dashboard to visualize predictions and identify inefficiencies.

## Future Work
- Incorporate production schedules and external factors like weather forecasts.
- Develop zone-specific models for granular insights.
- Extend the framework to support real-time predictions.