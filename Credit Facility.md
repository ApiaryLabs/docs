### 4. System Overview
#### 4.1 Credit Facility
The _Credit Facility_ allows users to access credit anytime, anywhere in a permissionless manner, in the form of $NECTAR. Upon depositing the approved reserve currency, the user receives an amount of $NECTAR as determined by Honeycomb’s _Credit Facility Smart Contract_. The deterministic algorithm within the smart contract is integral to the system, as it removes the need for human intervention, while reliably creating credit for its users. The combined reserve currency stored in the smart contract acts as the base money which will be used to determine the amount of _credit_ in circulation.  As Honeycomb welcomes more users, the value of $NECTAR will increase, increasing the total _credit money_ in circulation.

The Credit Facility Smart Contract is a continuous token model with a built-in liquidity mechanism that uses the concept of a bonding curve to create credit. $NECTAR can be minted or burned anytime by depositing or withdrawing the reserve currency to and from the smart contract. $NECTAR value appreciation is governed by the fixed reserve ratio, _r_.

###### Price of Nectar
$$
P = \frac{R}{Q_N\times r}
$$
As each subsequent reserve currency is deposited, it increases the supply of $NECTAR. The price of $NECTAR then continuously recalibrates so that the reserve ratio remains constant. The ratio selected determines the price sensitivity, which directly correlates to the amount of _credit money_ in circulation. 

###### Reserve Ratio
$$
r = \frac{R}{P\times Q_N}
$$
The reserve ratio is a fixed ratio between the QN × P and the total reserve currency locked in the smart contract, _R_. This ratio will be determined by the Honeycomb founding team, and takes on a range from $$0≤r≤1$$ which will always be held constant.

<p align="middle">
    <img width="600" alt="Credit Money" src="https://user-images.githubusercontent.com/102786818/163555087-b96ecb40-9046-4b47-99a4-c3bac7a4f5d7.jpg"/>
</p>


Scenario 1, $$r=1$$:  
When $$r=1$$, $NECTAR’s price remains constant and is independent of its supply. This implies that its value is pegged to the reserve currency. In other words, credit money is not created while $NECTAR becomes a proxy for the reserve currency. This can be likened to the gold standard, where the currency value is pegged to gold and can be exchanged for a fixed amount of gold.

<p align="middle">
    <img width="400" alt="Credit Money" src="https://user-images.githubusercontent.com/102786818/163705030-c456a1c4-6985-4c9f-8883-b82d4269fd0a.png"/>
    <img width="400" alt="Credit Money" src="https://user-images.githubusercontent.com/102786818/163705031-87c8973e-9b9f-41f4-b8ae-f88442adca01.png"/>
    <img width="400" alt="Credit Money" src="https://user-images.githubusercontent.com/102786818/163705034-7266e20d-8d91-426d-8f37-553a3fc7958e.png"/>
</p>


Scenario 2, $$r<1$$:  
When $$r<1$$, $NECTAR’s  price increases relative to an increase in reserve currency, resulting in credit money being created. This is similar to the current fractional reserve banking system we see today, where a fraction of the money in circulation is backed by actual cash on hand. The amount of excess credit created relative to the reserve currency is dependent on the reserve ratio. When $$r=0.5$$, $NECTAR’s price increases linearly with its supply, while $NECTAR’s price increases exponentially when $$r<0.5$$ and diminishes when $$r>0.5$$, as can be seen in the table above. 

##### 4.1.1 Minting $NECTAR
$$
q_n = Q_N(\frac{D_n}{R}+1)^r-1
$$
Anyone can acquire $NECTAR in exchange for depositing reserve currency, $$D_n$$. The amount of $NECTAR, qn received follows the algorithm above where the quantity received is determined based on the total supply of $NECTAR in circulation, $$Q_N$$ and the total reserve currency, $$R$$. The quantity of $NECTAR minted is reduced for each subsequent mint, as the amount of reserve tokens increases. Simply put, each subsequent $NECTAR minted becomes more “expensive”, and as such less $NECTAR is received for the same amount of reserve currency.

##### 4.1.2 Value of $NECTAR
$$
NV_n = Price_{NV} \times Quantity_{NV}
$$
Where:
$$
NV_n=-r.P.Q_N\times ((\frac{q_n}{Q_N}+1)^\frac{1}{r} -1)\times P_{reserveToken,30ma}
$$
The value of $NECTAR, $$NV_n$$ represents the value of $NECTAR each Honeycomb user holds. Its value does not follow the conventional bonding curve value, $$P\times q_n$$, as its immediate inflation may lead to undesirable behaviour, causing instability to the protocol. Instead, the value of $NECTAR is derived from the integral of the price function as seen below. This formula behaves so that the value of every newly minted $NECTAR approximately[^7] equals the reserve currency value at initiation. This way, it does not give bad agents the  incentive to cash out for immediate profit.The formula can be further broken down as such: 

$$
Quantity_{NV}=-r.Q_N\times ((\frac{q_n}{Q_N}+1)^\frac{1}{r} -1)
$$
The quantity component follows a concave relationship where $$Quantity_NV$$ experiences diminishing returns for every increase in $NECTAR the user holds. The unique concave property introduces unique implications in the Credit Swap Facility and will be further explained in section (4.3.2) below.

$$
Price_{NV}=P \times P_{reserveToken,30ma}
$$

The price component is derived by multiplying the price of the reserve currency, $$P_{reserveToken,30MA} with $NECTAR’s price, $P$, which follows a deterministic price movement. Given that the reserve currency is a non-stable coin, it will be exposed to price volatility observed in the crypto market. To circumvent this, the 30-day moving average price is used, so as to hedge against price volatilities that may result in unfavourable outcomes for Honeycomb stakeholders.


##### 4.1.3 Credit Money
Credit money is defined as the creation of monetary value in the financial system. In the current financial system, credit money is introduced through the fractional reserve banking system where commercial banks issue loans greater than the deposit they hold. The amount of credit money created depends on the reserves set by the Federal Reserve. Likewise, credit money is also determined by a reserve ratio, $$0≤r≤1$$.  However, credit money at Honeycomb Protocol is created through an algorithm rather than future claims.

As mentioned previously, the reserve ratio is decided by the Honeycomb founding team, and the value chosen has an impact on the amount of credit money created. A higher value of r results in less credit money created, while a lower value of r means more credit money is created. The chart below shows how much credit money is created based on the different reserve ratios. It can be interpreted as follows: On average, the amount of monetary value created is $$x$$ for every dollar of reserve.

<p align="middle">
    <img width="600" alt="Credit Money" src="https://user-images.githubusercontent.com/102786818/163556896-5b479681-366b-43f9-952a-dd7d1bf71f8f.png"/>
</p>

[^7]: It is approximate and not equal to the reserve currency value due to the use of the 30 day moving average. If the reserve currency is a stablecoin, the floor value will be equal to the reserve currency deposited.

##### 4.1.4 Exiting Honeycomb
Users of the protocol may choose to exit the protocol for any number of reasons. To do so, they may want to exchange their $NECTAR  for the reserve currency, or $COMB that can be easily traded outside of the protocol. In such an event, the user has two options to choose from:
1. Withdraw their Initial amount of reserve currency.
2. Choose to swap their $NECTAR for $COMB token via the Credit Swap Facility; refer to Section 4.3.1

Option 2 would be a dominant strategy in most cases as users are able to exchange their $COMB for a value that is more than their initial deposit, especially if their $NECTAR has appreciated in value. Since the value of $NECTAR uses the 30-day moving average price, there exists a possibility that $$reservCurrency_n>NV_n$$. In such a situation, some users may choose option 1 and withdraw their reserve currency as the payoff from doing so is higher at that point in time.

###### Withdrawal Fee
Withdrawal of the reserve currency imposes negative externalities on other Honeycomb users as it necessarily reduces the value of each user’s $NECTAR. To disincentivize consecutive redemptions, a withdrawal fee is introduced, with an algorithm that works to make each subsequent withdrawal of the reserve currency more expensive. The algorithm also deters “whales” from redeeming a majority of their $NECTAR at one time, as the amount of fees paid increases with the amount of $NECTAR redeemed.
$$
withdrawal fee = f + B(t)
$$

Similar to Liquity’s fee structure, Honeycomb’s withdrawal fee follows the formula above and is a function of the base rate, $$B(t)$$ and the fixed redemption fee, $$f$$ of $$1%$$. The fee is subtracted from the redeemed reserve currency, reducing the amount of reserve currency the user receives in return.

$$
B(t) = B(t - 1)_{\delta} + \alpha \times \frac{redeem_n}{Q_N}
$$

The base rate is a function of the previous base rate, $$B(t - 1)_{\delta}$$ and the redeemed quantity of $NECTAR relative to the total quantity of $NECTAR in circulation. During a redemption, the base rate is increased by the proportion of withdrawn $NECTAR and added to the previous base rate. At launch, the base rate is _initialized_ at 0.

$$
Decay Function: B(T-1)_{\delta} = B(T-1)\times \delta^{\Delta t}
$$

The previous base rate, $$B(t)$$ decays over time due to a decay factor, delta^{\Delta t} that is applied with every withdrawal prior to calculating the resulting fee. The magnitude of decay depends on the time that has elapsed, $$\Delta t$$ since the last redemption and $$\delta$$ is selected such that the base rate tapers to 50% after 12 hours. 