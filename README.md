This is a Python 3.0 project for analyzing stock prices and methods of stock trading using native Python tools and Google TensorFlow machine learning. It has two main class modules PriceTradeAnalyzer and SeriesPrediction described below.

Module: PriceTradeAnalyzer
Class PricingData
Given a stock ticker, this will go out and download historical price data from https://stooq.com.  I've had good success with this site.  The data set for ^SPX on stooq.com goes by to May 1, 1789 which is fairly comprehensive considering the index was created in 1926.  Downloaded data is cached to .csv file and stored in a Pandas dataframe which is easy to manipulate.  PricingData helper functions allow you to TrimToDateRange, ConvertToPercentages, NormalizePrices, CalculateStats (EMA, channels, momentum, etc), perform time frame graphing (using matplotlib), and a few other bells and whistles.  There are also several prediction models for predicting future prices.  Two options use the SeriesPrediction.py class to perform LSTM and CNN machine learning for their predictions.

EvaluatePrices.py shows how to use the PricingData class to PlotAnnualPerformance of a stock, DownloadAndGraphStocks for a list of stocks such as the S&P 500, CalculatePriceCorrelation of a list of stocks, OpportunityFinder to identify recent drops or over-bought/over-sold conditions from a list of stocks.

Classes Portfolio and TradingModel are used to test emulations of trading strategies.  EvaluateTradeModels.py shows examples of how to the TradingModel class to create and test trading strategies.  The models will use actual historical prices from PricingData. You specify the stocks you want to work with, the time frame you want to test against, and the logic you want to use for buying and selling.  Example strategies are included for BuyAndHold, Seasonal investing, and two different Trending approaches.  The resulting daily value and trade history are dataframes which are graphed and saved to .csv and .png files so you can view the performance details later.  ExtendedDurationTest allows you to test the performance of any model over various time frames and durations.  CompareModels allows you to compare the performance of any two models over a given time period.  I have yet to create a re-enforcement learning module using Deep Q or Policy Gradient.  That would be really great but I need to take a break and return to eating and sleeping on a regular basis.

Module: SeriesPrediction
Class StockPredictionNN uses LSTM (Long Short Term Memory) and CNN (Convolutional Neural Network) learning functions to predict future prices.  These use Google TensorFlow 1.5.0. The LSTM functions were adapted from Luka Anicin's https://github.com/lucko515/tesla-stocks-prediction.  The CNN functions were adapted from https://nicholastsmith.wordpress.com/ currency estimator and use his TFANN class wrapper for the TensorFlow implementation.

TrainPrices.py shows samples of using the StockPredictionNN class to train and test PricingData using LSTM and CNN machine learning techniques.

Special thanks to these people for helping me understand deep neural network machine learning:
Siraj Raval: https://www.linkedin.com/in/sirajraval/
Magnus Erik Hvass Pedersen: https://github.com/Hvass-Labs/TensorFlow-Tutorials
Nicholas T. Smith https://nicholastsmith.wordpress.com/ 
Luka Anicin: https://github.com/lucko515/tesla-stocks-prediction

I've tested this on both Windows 10 Python 3.6.4  and AWS Linux Python 3.6.2.  Both versions use TensorFlow 1.5.0.
Requirements: happily all native Python 3.6 and no C++ compilers
Windows PIP install requirements with:
pip install numpy
pip install pandas
pip install matplotlib
pip install tensorflow
pip install TFANN

AWS install requirements with:
python3 -m pip install numpy --upgrade
python3 -m pip install pandas --upgrade
python3 -m pip install tensorflow --upgrade
python3 -m pip install TFANN --upgrade

Note about using an AWS instance:  There is no GUI so I've added a switch to enable the Agg non-interactive back-end for matplotlib.  Also, it can be difficult to access web sites from within AWS as some sites block hosted IP ranges and python response headers, so I've added a web-proxy option to get around this.  We should bear in mind that the reason sites put these blocks in place is to avoid abuse of their services, so please be kind and don't abuse free services.

Have fun and keep programming!
-Tim
