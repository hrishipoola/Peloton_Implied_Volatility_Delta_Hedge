# Peloton's Implied Volatility & Delta Hedge

## Introduction 

Today, let's dig into Peloton (ticker: PTON). The purpose of this post is to:
- Forecast PTON's volatility at a point in the future by calculating its [implied volatility](https://www.investopedia.com/terms/i/iv.asp)
- Understand its option price sensitivities through the [Greeks](https://www.investopedia.com/trading/using-the-greeks-to-understand-options/) 
- Create a [delta-neutral](https://www.investopedia.com/terms/d/deltaneutral.asp) portfolio in which price decreases are wholly offset ([delta hedged](https://www.investopedia.com/terms/d/deltahedging.asp)) by a complementary increase in put option value.

In previous posts, we developed more realistic risk forecasts using GARCH models incorporating the time-varying character of volatility. Today, we'll calculate implied volatility for a point in the future using the Black Scholes model to back-calculate sigma based on the market price of a put option. One thing to keep in mind is that Black Scholes makes simplifying assumptions - price follows geometric Brownian motion, returns are normally distributed, zero transaction costs, asset pays no dividends, and risk free rate and volatility are constant. We'll show demonstrate that these assumptions don't actually hold in reality. For example, PTON's returns aren't normally distributed and that its implied volatility relative to strike price isn't constant (a straight line), but curves in a 'volatility smile.' Despite Black Scholes' limitations in option pricing, the model is still useful in practice for determining implied volatility and the Greeks. We could improve our estimates in the future with models that incorporate stochastic volatility (e.g., Heston model).   

We'll calculate the Greeks delta, gamma, vega (not actually a Greek letter), theta, and rho, which are option premium sensitivities (partial derivatives) with respect to specific characteristics of the underlying asset: 

- Delta: change in option price with \$1 change in underlying asset price (velocity) 
- Gamma: change in delta with \$1 change in underlying asset price (acceleration)
- Vega: change in option price with 1% change in implied volatility 
- Theta: change in option price with 1 day change in expiration (time decay)
- Rho: change in option price with 1% change in interest rate 	

We'll dive deeper into delta, looking at how it changes with time to maturity and delta hedging. We'll create a portfolio of Peloton stock and put options that's delta-neutral - that is, a decrease in PTON's price is wholly offset (hedged) by an increase in its put option value. Delta hedging is one strategy we can use if we believe an asset's price will increase long term, but, due to risks, could decrease in the near term. 

Before we dive in, let's unpack our investment thesis and options strategy for Peloton. 

## Investment Thesis

We're bullish on Peloton (ticker: PTON) in the 2-3 year timeframe due to a partial structural shift to in-home workouts, its app community and services, sticky user base (\<1% churn), increasing connected fitness subscriptions, strong cash position, and commercial sales potential in offices, hotels, and apartment complexes. While the upfront \$2500 dollars on a bike is a splurge for most, Peloton also offers 0% financing (through a 3rd party) amortized over 39 months. Not to mention the Apple acquisition rumors. Looking further out Peloton faces non-cycling product innovation pressure as customers aren't likely to make repeat bike purchases (currently, >80% of the company's revenue comes from product sales, not subscriptions). 

Over the next 6 months, Peloton faces supply chain and demand risks that could see its price decrease from its current rich valuation. Supply chain challenges have resulted in ongoing backlogs, recalls, and expenses. While Peloton's recent \$420 million acquisition of Precor and its 625,000 sq ft of U.S. manufacturing will help, it'll take time to integrate. CEO John Foley has stated that the company will need to invest in its supply chain for "years and years." Another near-term risk is moderating demand due to vaccine rollout and warmer weather.   

Put option strategy:

To protect against these downside risks on an existing PTON position, let's buy put options (right to sell) with a \$140 strike price that expires on June 18, 2021 after Peloton reports its fiscal Q3'2021 (calendar Q1'2021) earnings in May 2021. This would effectively give us a guaranteed floor price of \$140. With PTON's spot price currently at \$139, the put option is just about at-the-money with the spot price just about at the strike price (it isn't an aggressive or speculative position). If PTON's price is above \$140 on June 18, 2021, we simply won't exercise our option. If it's below \$140, we've guaranteed this floor price and protected against downside risk according to our risk tolerance. We'll see that at the $140 strike, the implied volatility is low and we believe it will go higher, meaning the option is undervalued and a good buy. Keep in mind, an options contract is for 100 shares of the underlying asset.  

We'll see at the end that combination of 170 shares of PTON and 4 put options (priced at $4.41 each) would get us to delta-neutral where any decrease in PTON's price would be offset by an equivalant increase in option value. 

If there's anything we could improve our if you'd like to share ideas, reach out! We've also included references at the end if you'd like to learn more. 









