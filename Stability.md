##### 4.2.3 $HONEY Stability
The primary objective of a currency is to maintain its stability so as to retain its purchasing power and to be adopted as a medium of exchange. This is achieved through trust in the system, where arbitrageurs can bring prices back to the peg by buying at a lower price and reliably redeeming for a profit if the peg breaks from the secondary market. However, if the trust in the redemption process breaks down, arbitrageurs may not participate, thereby causing the peg to break. Divergence from the peg is minimized through the stabilization mechanism and monetary interventions.

###### Stability Mechanism
For $HONEY to maintain its peg to the dollar, the liquidity facility must be sufficiently collateralized with $NECTAR such that borrowers are always incentivized to close their debt position, in an environment where creditworthiness is unknown. At the same time, the price volatility of the reserve currency needs to be taken into consideration. To overcome this volatility, three levels of stability measures are put in place to ensure $HONEY maintains its peg. The three levels are:
1. Margin Call  
 Margin call is the first line of defense and is triggered when the debt level of a user surpasses 90% of the credit line. The margin call notifies the user to reduce their debt level or improve their creditline by locking up more $NECTAR. 

2. Redistribution Mechanism  
$$
distribution Parameter_n = \frac{creditLine_n - Debt_n}{\sum{creditLine_n-Debt_n}}
$$

<p align="middle">
 <img width="450" alt="Before" src="https://user-images.githubusercontent.com/102786818/163706858-c43d50da-7f3c-4942-8ae0-40a1425036f5.png">
 <img width="450" alt="After" src="https://user-images.githubusercontent.com/102786818/163706859-e3eb3558-ca44-4236-80d2-0c3ddd68d7f7.png">    
</p>


 Redistribution is triggered when the borrower’s $$Debt_n>creditLinen$$. The smart contract will automatically close off the borrower’s debt position by redistributing the debt position to other existing debt holders based on the distribution parameter above. Concurrently, other debt holders will inherit the liquidated $NECTAR pro-rata as a compensation for taking on more debt, and they will experience a net positive benefit as the $$NV_n>creditLine_n$$.

 To prevent cascading liquidation, the distribution parameter prioritizes users with a healthier Debt-to-Credit ratio. Debt holders with a healthier Debt-to-Credit ratio will be better off as they will receive more $NECTAR tokens, giving users an incentive to maintain a healthy debt level. Similarly, the threat of liquidation and loss of potential appreciation of $NECTAR’s value incentivizes risky borrowers to improve their Debt-to-Credit ratio.

3. Circuit Breaker
$$
distribution Parameter_n = \frac{creditLine_n - Debt_n}{\sum{creditLine_n-Debt_n}}
$$
 To keep the total amount of $HONEY in circulation sufficiently collateralized[^9] in a time of crisis, the protocol incorporates a Circuit Breaker that prevents the Liquidity Facility’s health from falling below the critical threshold, TCDR<1. When Circuit Breaker is in force, all operations that would worsen the $$TCDR_N$$[^10] will be temporarily disabled. In this time, only the following actions are permissible:

 - Increase the credit line by collateralizing more $NECTAR
 - Reduce debt position by burning $HONEY

 This allows the system to activate Circuit Breaker at an earlier time, which is a safety precaution to ensure sufficient collateralization.

Should the execution of a particular level be unsuccessful, the next level will be triggered.


[^9]: In terms of $NECTAR value
[^10]: It is important to note that $$TCDR_N$$ incorporates the actual price of the reserve currency instead of the 30-day moving average, as the price of the $$reserveCurrency<reserveCurrency_30MA$$ during a bear market.

###### Monetary Intervention
Price of $HONEY in the secondary market may fluctuate due to market forces. In order to return $HONEY’s price back to its peg, the supply of $HONEY must be adjusted to meet liquidity demands, where:
- All else equal, an increase in economic activity will result in higher demand for $HONEY, pushing its price above the peg. By sufficiently increasing the supply of $HONEY, the price will return back to its peg.
- All else equal, a decrease in economic activity will result in lower demand for $HONEY, pushing its price below the peg. By sufficiently decreasing the supply of $HONEY, the price will return back to its peg.

###### Liquidity Converter
The Liquidity Converter smart contract’s willingness to respect the target exchange rate irrespective of market conditions keeps $HONEY closely pegged to the USD. An arbitrageur is able to achieve a risk-free profit when $HONEY deviates from its 1-dollar peg, while maintaining the stability of $HONEY. 
$COMB serves as the first line of defense against the price fluctuations of $HONEY through a Liquidity Converter. When:
- $HONEY < 1 USD, arbitrageurs can send 1 $HONEY to the Liquidity Converter and receive 1 USD worth of $COMB.
- $HONEY > 1 USD, arbitrageurs can send 1 $COMB to the Liquidity Converter and receive 1 $HONEY.

Intuitively, this is analogous to a form of monetary policy otherwise known as quantitative easing, where central banks buy and sell short-term bonds on the open market to add more liquidity into the banking system until interest rate targets are met.

###### Monetary Policy
The minting fee acts as a second line of defense, where the minting fee adjusts and scales relative to price deviation from the peg, to encourage or discourage the creation of newly minted $HONEY as mentioned above. When:
- $HONEY < 1 USD, it implies a contraction in economic activity.  The minting fee becomes more expensive disincentivizing the minting of $HONEY, bringing the $HONEY back to equilibrium.
- $HONEY > 1 USD, it implies an expansion in economic activity. The minting fee becomes cheaper, incentivizing the minting of $HONEY, bringing the $HONEY back to equilibrium.
This can be likened to the Federal Reserve adjusting interest rates, thereby making borrowing more or less expensive, so as to slow or stimulate the growth of an economy.
