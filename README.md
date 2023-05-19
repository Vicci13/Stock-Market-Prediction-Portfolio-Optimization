# Stock Returns Prediction & Portfolio Optimization
A research thesis entailing the prediction of stock returns using Long Short Term Memory (LSTM) neural network designs and portfolio optimization. Specifically, this study compares the prediction performance of a univariate and multivariate LSTM after which the return predictions from both models are fed into a mean variance optimizer and the final portfolios constructed are evaluated.

## Problem Statement
Classical portfolio optimization techniques often use historical prices and returns as model inputs which has limited influence on future stock behaviour therefore obtaining inaccurate estimates on future expected returns. 

Additionally, with the exponential increase in volumes of data, stock market analysts and particpants currently rely on non-AI methods (such as technical and fundamental analysis) for stock selection which are often arbitrary due to their limited ability to analyze raw data.

## Data 
10 year daily stock data (Open, Close, High, Low) from January 2013 to November 2022 for stocks listed on the Nairobi Securities Exchange (NSE). 

## Methodology
1. **_Data Cleaning and Preprocessing_** 
    - This entails ensuring the stock data has full price information for the 10 year period and removal of null or outlier values. 
    - An Augmented Dickey Fuller (ADF) test was applied to the stock returns to ensure time series stationarity. 
    - Data is then normalized within the range (0,1) and split into 80% for training and 20% for testing.
2. _**LSTM Model Construction**_ 
    - A Keras random search methoology was applied for both univariate and multivariate models to select the most optimal combination of LSTM hyperparameters. 
    - For the multivariate LSTM model, 167 features consisting of lagged versions of returns and technical indicators were generated. 
    - 25 features were selected as model inputs using Recursive Feature Elimination (RFE) via a Random Forest regressor.
3. **_Portfolio Construction_** 
    - 10 stock with the highest preidcted returns were selected for portfolio optimization. Here, 30-day return forecasts from each model were fed into a mean-variance optimization model. Portfolio performance metrics generated by each model's preditions were then compared. 

## Results 
#### LSTM Prediction Results 
The multivariate LSTM outperforms the univariate LSTM in returns prediction as evidenced by lower root mean squared error per predicted stock as well as by simply looking at the return prediction visualizations.

![SCOM univariate predictions](https://github.com/Vicci13/Stock-Market-Prediction-Portfolio-Optimization/assets/108093560/f486e5d0-c42e-42f1-9e22-aa1ba4b87b0f)
_Fig. 1: Univariate LSTM Return Predictions for Safaricom Data_

![SCOM multivariate predictions](https://github.com/Vicci13/Stock-Market-Prediction-Portfolio-Optimization/assets/108093560/7370ba12-e529-47cd-adb7-1ed0e2a4e474)
_Fig. 2: Multivariate LSTM Return Predictions for Safaricom Data_

The univariate LSTM model can be better used in classification and trend forecasting whereas the multifeature LSTM is more superior in actual value prediction. 

#### Portfolio Performance 
The univariate LSTM return-based portfolio model shows superior performance with a higher annualized Sharpe ratio of 5.592 compared to 0.667 for the multivariate return-based portfolio. 

![Optimum Uni-Portfolio Frontier](https://github.com/Vicci13/Stock-Market-Prediction-Portfolio-Optimization/assets/108093560/a97a0363-fbe2-4b06-baa2-1d051428c304)

_Fig. 3: Efficient Frontier for Univariate LSTM-Based Portfolio_


![Optimum Multi-Portfolio Frontier](https://github.com/Vicci13/Stock-Market-Prediction-Portfolio-Optimization/assets/108093560/090e5f89-8793-45d5-aedf-1d2a034d85d6)

_Fig. 4: Efficient Frontier for Multivariate LSTM-Based Portfolio_

While achieving excess returns excess returns to risk is paramount for any portfolio past studies emphasize on prediction accuracy as a crucial aspect for asset preselection. On the basis of having more accurate stock return predictions, the study recommends the multifeature LSTM for stock forecasting and subsequent portfolio optimization. 
