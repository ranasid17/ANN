# Financial Mathematics 

1) Repository containing various programs created in order to better inform and predict stock market trading 
2) 8/2019: perceptron is a 1 layer perceptron that given an input matrix (X) and the correct output (Y), attempts 
    to predict whether the binary output should be [0,1] 
3) 10/22: twoDayChange is a class that given a CSV of historic data, calculates the relative price change of that 
    instrument's 48h performance (Monday-Wednesday of each week) and then plots a probability function of the 
    relative changes. Documentation within the class indicates how to pass arguments and interpret outputs of each 
    method. Each method should be used sequentially within class. 
4) 12/22: simpleMovingAvg is a class that pulls historical data of a ticker from YF to calculate long and short 
    term MAs of the security. It then plots both on top of the underlying price. When the short term MA crosses 
    over the long term MA, it is a (potential) signal to buy (vice versa for when short term MA crosses below). 
