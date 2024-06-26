# Pair Trading Strategy

Pair trading strategy is when the ratio 2 highly correlated and cointegrated stocks, diverage from their mean due to some underlying conditions ie, market volumne, insider information and market changes. Since the 2 price series are cointegrated, we can safely assume that the prices will converge back to their mean. 

Rather than correlation, we will be picking our stocks based on **cointergration**. 

In our strategy, we will be primarily using 3 types of ratio to help generate signals for our positions
1. RAW_RATIO: Raw Price Ratio of 2 stock prices<br>
***Raw Ratio Z-score = (Price Ratio - Mean of Price Ratio) / Standard Deviation<br><br>***

2. MA_RATIO: Simple Moving Average Ratios based on 2 stock prices<br>
***MA Ratio Z-score = (MA<sub>Short Term</sub> - MA<sub>Long Term</sub>)  / Standard Deviation<sub>MA Long Term</sub>*** <br><br>

3. ATE_RATIO: ATR Spread Ratio based on 2 stock prices<br>
*ATR Spread = ATR<sub>Ticker_1</sub> / ATR<sub>Ticker_2</sub><br>*
*ATR Ratio = (Price<sub>Ticker_1</sub> / Price<sub>Ticker_2</sub> ) * ATR Spread<br>*
***ATR Ratio Z-Score = (ATR Ratio - Mean<sub>ATR Ratio</sub>)  / Standard Deviation<sub>ATR Ratio</sub><br><br>***


These 3 variations of the strategy will be defined by the Strategy_Type Emun Class as shown below

By normalising the price ratio generated by the desired strategy variation, we will be able to generate signals based on the normalised spread.

In the Pair Strategy Class, we will be setting the signal thresholds for each variation and once the price ratio is within **±0.05**, a long or short position will be open.

For example, if the given threshold is 1:
1. Given price ratio is **-1.04** (within -0.05 of threshold), a long signal is generated on the price ratio graph and we will **Long** ticker_1 and **Short** ticker_2<br>
2. Given price ratio is **1.04**(within +0.05 of threshold), a short signal is generated on the price ratio graph and we will **Short** ticker_1 and **Long** ticker_2\

All positions of the pair will be closed if the price ratio is within **±0.05**
