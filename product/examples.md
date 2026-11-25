# Examples

Two loans with the same amount, LTV and rate. The borrower takes $10,000 in USDC at an LTV of 60%, so the collateral is worth $16,667. The term is about one year and the rate is 7% per year. One loan is against tokenized Apple stock, the other against Bitcoin.

| | Apple | Bitcoin |
|---|---|---|
| Collateral | 47.0 shares | 0.2651 BTC |
| Term | 387 days | 315 days |
| Put price | $230, 65% of the market price | $40,000, 64% of the market price |
| Interest to lenders, 7% per year | $742 | $604 |
| Put premium | $266, 2.5% per year | $453, 5.2% per year |
| **Cost without a call** | **$1,008, 9.5% per year** | **$1,057, 12.2% per year** |
| Call price for a 4.5% effective rate | 29% above the market price | about 50% above the market price |
| Call price for a 0% effective rate | 17% above the market price | about 34% above the market price |

## Apple

Of the 9.5% per year, 7.0% is the rate that lenders earn and 2.5% is the put. If the borrower sells a call at $416, which is 17% above the market price, the call premium covers both the interest and the put. The borrower pays no cash and keeps Apple's gains up to that price. Gains above it go to the buyer of the call.

## Bitcoin

Bitcoin moves more than Apple, so its put costs more, 5.2% per year on top of the same 7.0% rate. Its calls pay more too. A call at about $84,000, which is 34% above the market price, covers the whole cost.

{% hint style="info" %}
The numbers are an illustration based on listed option prices, without fees or gas. The loan buys its options on its own venue, where premiums can differ.
{% endhint %}
