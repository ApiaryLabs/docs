#### 4.2 Liquidity Facility
The _Liquidity Facility_ follows an over-collateralized model[^8] we see in the current DeFi ecosystem where decentralised stable coins are minted. It is integral to the ecosystem as it provides users with easy access to liquidity in the form of a stable coin, done in a trust-less manner. Trust is achieved through the transparency of the blockchain, effective management of risk and an incentive structure that ensures stability of the protocol and $HONEY.

Honeycomb users can realize their credit anytime through the liquidity facility by collateralizing their $NECTAR and paying a variable mint fee in the form of $COMB. In exchange, the user receives $HONEY, the value of which is pegged to the USD.

As $HONEY is minted against $NECTAR, Honeycomb defines $HONEY as debt owed to the protocol. Hence, the minting of $HONEY is recorded as debt. At all times, the user’s debt cannot exceed their [credit line](https://www.investopedia.com/terms/l/lineofcredit.asp)[^7], else they will risk losing their collateralized $NECTAR. Risk-averse users are encouraged to mint $HONEY based on their needs, so as to hedge against the loss of their $NECTAR. In order to retrieve their $NECTAR, the debt position must be closed off by burning $HONEY through the Credit Facility Smart Contract.

[^7]: A line of credit is a defined amount of money that you can access as needed
[^8]: Note that $HONEY is under-collateralized in terms of the reserve currency. However, the underlying strategy is over-collateralized through $NECTAR

##### 4.2.1 Minting of $HONEY
To mint $HONEY, users will lock their $NECTAR into the _Liquidity Facility Smart Contract_. The amount of $HONEY users are allowed to mint is based on the user’s credit line. A user’s credit line is calculated as a function of his deposit and a multiplier as seen below.

$$
creditLine_n = M_n \times D_n
$$


| Tier | Multiplier |
| - | :-: |
| 0 | $$ M_n = \begin{cases} \frac{NV_n}{D_n},& where& \frac{NV_n}{D_n}<1 \end {cases} $$
| 1 | $$ M_n= \begin{cases} 1,& 1≤\frac{NV_n}{D_n} <1.1\\ 1.1,& 1.1≤\frac{NV_n}{D_n} <1.2\\ 1.2,& 1.2≤\frac{NV_n}{D_n} <1.3\\ 1.3,& 1.3≤\frac{NV_n}{D_n} <1.4\\ 1.4,& 1.4≤\frac{NV_n}{D_n} <1.5\\ 1.5,& 1.5≤\frac{NV_n}{D_n} <1.6\\ 1.6,& 1.6≤\frac{NV_n}{D_n} <1.7\\ 1.7,& 1.7≤\frac{NV_n}{D_n} <1.8\\ 1.8,& 1.8≤\frac{NV_n}{D_n} <1.9\\ 1.9,& 1.9≤\frac{NV_n}{D_n} <2 \end {cases} $$ |
| 2| $$ M_n= \begin{cases} 2,& 2≤\frac{NV_n}{D_n} <2.2\\ 2.2,& 2.2≤\frac{NV_n}{D_n} <2.4\\ 2.4,& 2.4≤\frac{NV_n}{D_n} <2.6\\ 2.6,& 2.6≤\frac{NV_n}{D_n} <2.8\\ 2.8,& 2.8≤\frac{NV_n}{D_n} <3\\ \end{cases} $$
| 3 | $$ M_n= \begin{cases} 3,& 3≤\frac{NV_n}{D_n} <3.25\\ 3.25,& 3.25≤\frac{NV_n}{D_n} <3.5\\ 3.5,& 3.5≤\frac{NV_n}{D_n} <3.75\\ 3.75,& 3.75≤\frac{NV_n}{D_n} <4\\ \end{cases} $$
| 4 | $$ M_n= \begin{cases} 4,& 4≤\frac{NV_n}{D_n} <4.5\\ 4.5,& 4.5≤\frac{NV_n}{D_n} <5\\ \end{cases} $$
| 5| $$ M_n= \begin{cases}  5,& where& 5<\frac{NV_n}{D_n} \end {cases} $$ 




The multiplier follows a tiered level system that is based on the credit-to-deposit ratio (CD Ratio). The multiplier grows as more users join the Honeycomb protocol. Note that $$NVn≥creditLine_n$$, which implies a margin of safety to account for volatility in the value of $NECTAR.

##### 4.2.2 Minting of $HONEY
Minting fee is introduced as a form of “monetary policy” to govern the supply of $HONEY in circulation. It is also implemented as a form of friction to deter Honeycomb users from minting out more $HONEY than they should, which will lead to instability in the liquidity facility. The fee is designed such that it increases as debt increases and only those with a higher willingness to pay will mint out more $HONEY. The minting fee follows the formula below.

$$
Mint Fee = \frac{(Debt_{n,t-1}+Debt_{n,t})^{\alpha}}{Threshold_n} + \frac{Debt_N^{\beta}}{R} \times peg
$$

where:

$$
Threshold_n = (1 - r + \frac{D_n}{P\times q_n}) \times r.P.q_n
$$

The minting fee is a function of the individual’s debt accrued, the overall debt in the system and the peg between $HONEY and the US dollar. $$Threshold_n$$ is an algorithmic driven variable that determines when the minting fee starts to scale, such that the sum of each user’s threshold equals the to reserve currency.  and  represents the sensitivity parameter of each component. The peg is a parameter that either decreases or increases the mint fee based on the market forces of $HONEY, so as to encourage or discourage users from introducing more supply into the market. More on that in section 4.2.3 under _Monetary Policy_.

