# benchmark
Time Series Forecasting: SARIMAX vs Attention LSTM
 Project Overview
The complete Python implementation for dataset generation, preprocessing, SARIMAX baseline modeling, Attention LSTM training, hyperparameter tuning, cross-validation, and evaluation is provided in the accompanying Jupyter notebook (bench.py). All experiments are fully reproducible by executing the notebook end-to-end.
The objective is to:
•	Ensure reproducibility
•	Apply rigorous time-series validation
•	Provide quantitative and comparative results
•	Analyze model interpretability
Dataset Generation
 Dataset Characteristics
•	Observations: 1000
•	Target variable: Continuous time-series
•	Exogenous features: 4
•	Components:
o	Linear trend
o	Sinusoidal seasonality
o	Gaussian noise
Data Generation Code
trend_slope = 0.05
seasonal_amplitude = 10
seasonal_period = 24
noise_std = 2.0
The dataset is saved as:
synthetic_timeseries.csv
Models Implemented
Baseline: SARIMAX
Final Configuration:
•	Non-seasonal order: (p, d, q) = (1, 1, 1)
•	Seasonal order: (P, D, Q, s) = (1, 1, 1, 24)
This configuration was selected after manual grid search over a constrained parameter space.
SARIMAX PERFORMANCE
MAE: 3.054081633495519
RMSE: 3.7831695296665666
Advanced Model: Attention LSTM
The Attention LSTM learns temporal dependencies and assigns importance weights to time steps, improving interpretability and long-range dependency modeling.
Architecture:
•	LSTM hidden units: 64
•	Attention mechanism: Softmax-based temporal weighting
•	Loss: Mean Squared Error (MSE)
•	Optimizer: Adam
Attention Performance
MAE: 0.129720946060467
RMSE: 0.16302488983528995
Validation Strategy
Train–Test Split
•	80% training
•	20% testing
•	No shuffling (time order preserved)
Cross-Validation
•	Rolling-window cross-validation
•	Implemented using TimeSeriesSplit
•	5 folds
This avoids information leakage and simulates real-world forecasting scenarios.
       AVERAGE  MAE	                           AVERAGE    RMSE
               1.65	                            2.06
Hyperparameter Optimization Strategy
Although Bayesian Optimization was initially suggested in the prompt, manual grid search was chosen due to:
•	Small, well-understood SARIMAX parameter space
•	High computational cost of repeated deep learning training
•	Need for transparency and reproducibility
This approach was sufficient for a controlled synthetic dataset and ensured stable convergence.
Model Interpretability
Interpretability Findings
Attention weight visualizations show that the model assigns greater importance to recent observations while still leveraging longer-term context. This indicates effective learning of short-term dependencies and seasonal patterns.
Predictive Strengths
•	Captures nonlinear and multivariate temporal relationships
•	Adapts dynamically to evolving patterns
•	Stable performance across cross-validation folds
Predictive Weaknesses
•	Higher computational cost than SARIMAX
•	Sensitivity to hyperparameter selection
•	Less transparent than coefficient-based statistical models
Visualizations
The notebook includes:
•	Actual vs Predicted plots for test data
•	Attention weight heatmaps
•	Printed evaluation and comparison tables
 Conclusion
This project demonstrates a rigorous benchmarking framework for time series forecasting. While SARIMAX offers simplicity and interpretability, the Attention LSTM provides greater flexibility and modeling capacity for complex multivariate data. The choice between models should be guided by data complexity, interpretability needs, and computational constraints.





