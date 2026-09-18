Harshel Gopiinaath
z5764696 UNSW

# ml-volume-imbalance-predictor
A trading strategy that attempts to use features built from the concept of resting order book volume imbalance to predict short term price direction of BTC 
with binary classification.

In this project, I used XGBoost in Python to train a gradient boosted tree model on trade flow features and order book imbalance to determine whether price goes
up or down in a short time horizon. I used data from Kaggle via kagglehub (martinsn/high-frequency-crypto-limit-order-book-data) and took the price of BTC
in 1 minute snapshots to build features. Namely, I used the midpoint, spread, buys, sells and bids/asks notional columns to build a number of features.

The features I built were imbalance, taking best bid vs best ask imbalance, multi level imbalance including the aggregate of all 15 order book levels,
rolling imbalance with smoothing of noise via a 20 snapshot rolling average, momentum, trade imbalance and spread. Then, I trained on the binary target of 
whether midpoint rose over 10 snapshots (1 output) or not (0 output), which was taken as a reasonable short term window rather than systematically optimised.

I also split data chronologically 80/20 to train on old data and test on relatively new data, assessing the accuracy of my model.

The main limitations with this project included the single asset/timeframe testing as well as the lack of slippage and transaction costs being modelled - 
this training sample may not work on other assets and so features should be adjusted depending on what is being traded. Furthermore, there exist unoptimised 
paramters and thresholds which may throttle profitability. Finally, and most importantly, the binary classification disregards how the magnitude of the price will change.

I intend on taking this project further and potentially moving past a binary classifier to try predict magnitudes as well, and ideally wish to find optimised parameters
that may increase chances of real world profitability. Modelling slippage and transaction costs is also something I hope to achieve soon.
