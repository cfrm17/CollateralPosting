# Collateral Posting

In this collateral method, derivative trades and the collateral assets are handled similarly. They are deemed as two “sub-portfolios” with opposite trade direction. Their future value distributions are calculated under the same Monte Carlo simulation framework. All risk factors are simulated simultaneously and consistently.

This collateral method is built on a mixture of backward and forward looking style. The counterparty exposure is measured on a date when the counterparty is deemed to be in default. This is consistent with the terminology and concept of “Exposure at Default” in CCR. Standing at a reporting time bucket t, the collateral assets has been posted in the past, and the collateralized exposure depends on the “liquidation” value of the derivative portfolio and collateral assets at some future time. 

When the Bank determines that the counterparty is in default, it will start to negotiate new trades to replace exist derivative portfolio. At the same time, it will take hold the collateral asset and try to sell these assets in the market. The value fluctuations of the portfolio and the collateral asset during their liquidation periods create risk to the Bank. In a CCR model which inherently incorporates the Wrong Way risk, both trades and collateral assets liquidation value need to be calculated conditional on the fact that the counterparty is in default.

Although our method is logically more consistent with the counterparty exposure definition, it can also be changed by “shifting” the exposure calculation time t along the timeline. If the time t is set at the end of the liquidation (or closeout) period, then we have a backward looking model. Or if t is set at the beginning of the settlement period, we will have a forward looking model.

Before time t when the counterparty is deemed to be in default, there is usually a “special” time interval called the settlement period (or grace period). The grace period is given to the counterparty to pay trade premium/coupon, or post more collateral assets. Under the business conversion, the settlement period may last for a few days. It is assumed that during the settlement period:
 
·         The counterparty does not post more collaterals (if called), or does not return over-posted collateral by the Bank
·         The Bank posts more collateral to the counterparty,  or returns over-posted collaterals to the counterparty
·         The counterparty does not pay premium/coupon to the Bank
·         The Bank pays premium/coupon to the counterparty

The coupon is the nominal annual rate of interest that is paid to the bondholder on a regular basis. It is usually expressed as a percentage of the face value (coupon rate). The coupon rate is either fixed or variable. The coupon rate is given as an annualized percentage of the face value. See https://finpricing.com/lib/FiBondCoupon.html

These assumptions are made for the “worst” cases so that the counterparty exposure is more conservative. In the better situation, the counterparty may continue to fulfill the deal payments and collateral calls until the sudden default. On the contrary, if the counterparty fails to make the payments during the grace period, while the Bank could not recognize the counterparty default and take procedures to liquidate the trades, the exposure may become higher than what the model implies.
 
The OTC trade settlement period can be defined at the trade level. The information is defined as a trade attribute, or determined according to some mapping rules (e.g. by trade type). length of settlement period should be defined at the counterparty level, and should be allowed to change under different conditions (e.g. special economic environment or for stress testing purpose).
