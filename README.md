# Financial Mathematics 

This repository containing quantitative analysis programs created in order to better inform and predict stock market trading. These programs are primarily used to trade short-term options. I included a mock spreadsheet (coming soon) that is structured to log weekly trades and their returns. **tradingAnalysisMethods.py** is a program containing classes and methods useful to analyze the weekly trades placed by an options trader in order to understand their returns in comparison to the S&P500. These methods are executed in **weeklyAnalysis.py**. 

## 1) perceptron.py
This is a 1 layer perceptron that accepts an N x N input matrix (X) the user defines, and a 1 x N output matrix (Y) which contains the correct output for each row of X. The perceptron attempts to predict the value of Y for each row. 

For example, if passed X = [0 0 1; 1 0 1; 0 0 0] and Y = [1; 1; 0] the goal is for the 1-layer neural network to predict as close to Y as possible. Perceptron.py will produce a binary output bewteen [0,1] for each row in its 3x1 output that increases in accuracy as the number of training epochs increases. The 1-layer neural network is primarily intended to demonstrate how non-traditional machine learning can predict quantitative data.  
## 2) twoDayChange.py**
This is a class that passed CSV of a security's historic data, calculates the relative price change of that instrument's performance over a sliding window (ex: Monday-Wednesday of each week for the past year). It then calculates the probability, using kernel density estimation (KDE), of the relative prices changes over each window and plots the result. The underlying probability density function (PDF) estimated by KDE theoretically provides greater accuracy and insight into the security's price change than simply viewing the actual probabilities. 
    
By knowing the underlying PDF, price change peaks and deviation, short term options can be traded around the security's price movement during sliding window. Documentation within the class indicates how to pass arguments and interpret outputs of each method. Each method should be used sequentially within class. 
## 3) simpleMovingAvg.py 
This is a class that pulls historical data of a ticker from YahooFinance to calculate long- and short-term MAs of the security. It then plots both MAs alongside the underlying price. When the short term MA crosses over the long-term MA, this is a signal to buy the security (due to positive momentum). Conversely when short-term MA crosses under the long term MA, this is a signal to sell the security (due to negative momentum). S/LT MA windows can be modified from default setting (50/100). 

I prefer 20/50 ST/LT MAs because in my experience it provides the best balance between noise reduction of recent price changes in volatile markets while also allowing for some flexibility in weighting the most recent price changes. 
## 4) LSTM.py 
This is a long short-term memory neural network that uses historical data from a security in order to predict the next day average price. LSTM neural networks are likely the best type of architecture to predict time series data due to their recurrent structure which allows for prior time values (in this case stock prices) to be refeed into the base layer as parametrized. The current iteration of this can predict next-day NASDAQ index (the top 100 stocks listed on NASDAQ) to about 96% accuracy. Running this model nightly would theoretically allow a trader to accurately asses risk and price the valuation of short term (next day expiry) contracts on any security that tracks the NASDAQ index.  
    
LSTM.py also includes methods to predict next day price from simple MA and exponential MA models with the associated visualization and error calculation. I included these methods because the average run time to train LSTM.py is about 6h. Usually running this at night provides ample time to analyze the results before market open at 9:30a EST, and then place trades in the morning. However on nights when this is not possible, ST/LT MA analysis (similar to simpleMovingAverage.py) and its derivative, exponential moving average (EMA), may allow for accurate trades. 
## 5) tradingAnalysisMethods.py 
This is a file containing data engineering and analysis classes utilized in weeklyAnalysis.py. 
 
The **preprocessing** class contains data engineering methods to load a downloaded CSV file (from an AirTable database) and clean the values for analysis. *clean_df* loads a local CSV and removes extraneous symbols to allow for downstream processing. *extract_trading_weeks* accepts the cleaned data frame from *clean_df* and pulls a list of trading weeks from it. The output list is analogous to the YTD Sundays. The list of YTD weekdays can be extracted from the *pull_weekdays* function; at the moment it only returns Mondays and Fridays (start/stop of trading weeks). 
 
The **trading_analysis** class contains 3 methods to extract information from the data frame necessary for downstream analysis and visualization. *revenue* accepts the data frame and list of trading weeks to return the weekly revenue (dollar amount) from all trades placed within a trading week, the cumulative revenue - found by summing each week's revenue, and the adjusted cumulative revenue which accounts for various fees and commissions associated with trading options. *ROI* is similar to revenue in inputs and outputs but considers the percent weekly return rather than dollar amount. *balance* accepts the same input arguments as *revenue* and *ROI* but returns the total cash balance at the start of each trading week. 
 
My options trading is an attempt at active trading in order to beat the (average) returns of "the market". Therefore it is important to define the benchmark which I am competing against. I have chosen the S&P500 ETF (SPY) as my benchmark due to its high liquidity, correlation to the S&P500, and widespread acceptance as a benchmark. **spy_analysis** contains methods to extract the weekly open and close price (*get_monday_friday_prices**), calculate the weekly value change/ROI of SPY (*weekly_value*), and then store is information in a dataframe (*create_dataframe*). 
## 6) weeklyAnalysis.py 
I have segregated the function calls to analyze the weekly options trading I run into **weeklyAnalysis.py** in order to promote readability in my code.  
 
    
