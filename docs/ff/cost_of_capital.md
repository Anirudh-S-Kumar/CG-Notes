## Preference Shares

Preference shares are a type of share that pays a fixed dividend before any dividend is paid to ordinary shareholders. If the company goes bankrupt, preference shareholders are paid before ordinary shareholders. Most preference shares have a fixed dividend, while common shares have a variable dividend. Preferences shares do not hold voting rights in the company, but ordinary stocks do.

There are mainly 4 types of preference shares:

- Cumulative (guaranteed)
- Non-cumulative 
- Participating
- Convertible

## Weighted Average Cost of Capital (WACC)

$$\text{WACC} = w_d k_d (1 - T) + w_p k_p + w_e k_e + w_{re} k_{re}$$

Where

| Term | Description |
| --- | --- |
| $w_d$ | Weight of debt |
| $w_p$ | Weight of preference shares |
| $w_e$ | Weight of equity |
| $w_{re}$ | Weight of retained earnings |
| $k_d$ | Pre-Tax Cost of debt |
| $k_p$ | Cost of preference shares |
| $k_e$ | Cost of equity |
| $k_{re}$ | Cost of retained earnings |


## Bonds 

- Security that obligates the issuer to make specified payments to the bondholder over a period of time.
- Face Value, Par Value: The amount the bondholder will receive when the bond matures.
- Coupon Rate: The interest rate that the bond issuer will pay to the bondholder.
- Zero-Coupon Bonds: Bonds that do not pay interest during the life of the bond, let you buy the bond at a discount and receive the face value at maturity.

### Bond Yields

| Term | Description |
| --- | --- |
| Nominal Yield | Annual Coupon rate |
| Current Yield | Annual Coupon rate / Current Price |
| Yield to Maturity (YTM) | Discount rate that makes present value of bond's payments equal to its price |
| Premium Bond | Bond that sells for more than face value |
| Discount Bond | Bond that sells for less than face value |

??? Example

    > A Rs. 1000; 10% bond with 2 years to maturity selling in the market at Rs. 980.

    Nominal yield: 10%

    Current Yield : 100 / 980 * 100 = 10.2%

    $$980 = \frac{100}{(1 + YTM)^1} + \frac{100 + 1000}{(1 + YTM)^2}$$

    Comes out to approx 11.17%

## Common equity

Two kinds of common equity:

- Retained earnings(internal common equity)
- Issuing new shares of common stocks

To estimate the cost of equity, there are 3 methods:

- Dividend Discount Model
- Capital Asset Pricing Model (CAPM)


- Risk Premium Approach

$$k_e = k_d + rp_e $$

### Dividend Discount Model

$$k_e = \frac{D_0(1 + g)}{P_0} + g$$

The value of the stock today is the present value of all the dividends that the stock will pay in the future.

$$P_0 = \sum_{t=1}^{\infty} \frac{D_t}{(1 + r)^t}$$

Where $D_t$ is the dividend paid in year $t$, $P_0$ is the current price of the stock, $r$ is constant cost of equity capital

If we assume constant growth rate $g$, then cost of equity can be calculated as:

$$k_e = \frac{D_0(1 + g)}{P_0} + g$$

??? Example

    The market price of a share of common stock is Rs.60. The dividend just paid is Rs.3, and the expected growth rate is 10%.

    $$k_e = \frac{3(1 + 0.1)}{60} + 0.1 = 0.155 = 15.5%$$

### Capital Asset Pricing Model (CAPM)

$$k_e = R_f + \beta (R_m - R_f)$$

Where $R_f$ is risk-free rate of return, $R_m$ is return on market portfolio, and $\beta$ is measure of risk.

??? Example

    > $\beta = 1.2$, $R_f = 5%$, $R_m = 13%$

    $$k_e = 0.05 + 1.2(0.13 - 0.05) = 0.05 + 0.096 = 0.146 = 14.6%$$

### Risk Premium Approach

Adds a risk premium to the bondholder's required rate of return.

$$k_e = k_d + rp_e $$

Where $k_d$ is the required rate of return on debt, and $rp_e$ is the risk premium for equity.


### Cost of New Common stock

If retained earnings are not enough, the company can issue new common stock. Dividend Growth Model must adjust for floatation costs.

$k_{cs} = \frac{D_1}{P_0(1 - F)} + g$

Where $F$ is the floatation cost.

### How to find $g$?

$g$ is the growth rate of dividends or earnings.

$g = (1 - payout ratio) \times ROE$

Where payout ratio is the proportion of earnings paid out as dividends, and ROE is the return on equity.

