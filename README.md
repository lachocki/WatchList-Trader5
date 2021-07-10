# WatchList-Trader5
Alrighty this is the project closely following Trader3 which you can also find on my GitHub profile. You might be wondering what happened to Trader4, lets talk some quant trading. So Trader3 could be defined as a intraday swing trading methodology. When it was profitable, the margin was anywhere from 0.25% to 1%+ which is pretty nice, but where we were losing money it would often wipe out any gains hence the creation stoploss function. I saw this as an oppoptunity, no trading algorithm is perfect, but I saw a clear pattern that could allow me to capitalize on the times we would usually would lose money on Trader 3. This pattern was essentially a momentum pattern. So as quickly as possible I wrote Trader4, a hedging momentum methodology. It would start by buying both 3x leveraged sides of the ETF QQQ. At that point, any loss would be roughly offset by a gain of a similar size. I would continue to hold them until noticing a momentum trend than I would dump the loser (the one with the lower RSI, regardless of whether it was the one I was making or losing money on). Then I would track the winner up, with the goal of offsetting the loss, plus profits, with the additional momentum of the winner. In four days I had a working, mainly debugged version than realized "Shoot, this is superfluous. All it really achieves is a momentum strategy with only half of my liquidity. I might as well just make a dedicated momentum methodology minus the unnessary hedging." 

This was the genesis of Trader5, a momentum trading methodology to attempt to capture gains from the times there was no swing in the intraday trading. I knew going into Trader5 that its win rate would be roughly the same as Trader3s'. But that was no big deal because Trader6 would be a blend of the two methodologies optimized to figure out which methology to go with at any given time based on some data. It was my goal to find that data but I got sidetracked by a recurring idea with new evidence of doability. That is still what I'm working on. Trader6 will come eventually with the added benefit of what I'm working on right now.

Anyways, this is Trader5 let's get started.

It is designed to trade in any market conditions by utilizing 3x leveraged ETNs that have both a 'Bull' and 'Bear' version so you can bet for or against the market at any given point in time.

Any personal information will be left out of the code and replaced with a copious amount of Xs :) I would recommend saving this file to somewhere out of reach of GitHub so any changes you make to it CAN'T be seen by others! I think that's how that works. Below I'll walk you through how and where to replace information so you can get it running for yourself! But first.

Install & Dependencies: Below are the 3 packages that are somewhat unusual that the algorithm needs to be able to place trades, get data, and send SMS notifications. Otherwise most packages you'll see are pretty ordinary (os,time,pandas,etc.) Note that this algorithm is made for trading on a RobinHood brokerage account. within the Robin-Stocks module you can use it for other brokers but this one is strictly set up for RobinHood.

pip install robin-stocks

pip install finnhub-python

pip install twilio

Next up I use a few different .csv files to store data: Trader_Returns.csv (Where I monitor my returns for column headers reference line 606, percMovements.csv (which stores the relative speed of an interval of trading AND is attached to this so you dont have to run all of your own data), StockOrders.csv (is the result of pulling my orders from the Robinhood API, reference line 564.

Next up, changing information to your own! On line 27 you'll want to change the text with in the quotes to your one time password (OTP) which Robinhood will give you once you set up Two-Factor Authentication (2FA) which the documentation for the Robinhood API can walk you through at https://robin-stocks.readthedocs.io/en/latest/quickstart.html

On line 37 replace the Xs with your phone number and make sure to include the international code +1 if you live in the U.S.

On line 47 replace the Xs with your Finnhub API key, one of which can easily be obtained at https://finnhub.io for free and its worth noting the way my algorithms are setup they are optimized to not run over Finnhub's API data pull limit.

On line 51 you'll define the path which is referenced on line 564 to your working directory where you have a Trader_Returns.csv to monitor returns.

On lines 48 and 49 these act as your API keys for Twilio services which will send you text messages throughout the trading process. You will have to set this up on your own but Twilio does a great job showing you how to do so! It does cost money but it's less than a penny per SMS (USD). Once you have these keys enter them as environmental variables for added security.

Lastly, on line 54 you can change 'overall_percent' to your liking. It controls how much of your available account cash you want to use for a given trade. For Trader5 I left in the 'profitSell' item on line 55 (something I took off on Trader3) just in case somebody wants to lower the dollar amount after a winning trade.

Once, you have all of this set, you should be good to go for this methodology!
