Capital Investment is any investment for which the economic benefit is greater than one year. Capital budgeting is a process that companies use for decision making on capital projects - those projects with a life of one year or more.

Broad steps to do capital budgeting:

- Estimate Cash Flows
- Assess riskiness of CFs (we will not consider this here)
- Determine the appropriate cost of capital
- Find NPV(Net Present Value) and/or IRR(Internal Rate of Return)
- Accept if NPV > 0 or
- IRR > Required rate of return(WACC - weighted average cost of capital)

NPV is the difference between the present value of cash inflows and the present value of cash outflows over a period of time. It is used in capital budgeting to analyze the profitability of an investment or project.

## Independent vs Mutually Exclusive Projects

==Independent projects== : If the cash flows of one are unaffected by the acceptance of the other.

==Mutually exclusive projects== : If the cash flows of one can be adversely impacted by the acceptance of the other.

??? Example "Explained through an example"

    Company allocates a budget of Rs.60,000 for expansion

    | Project | Cash Flows |
    |---------|------------|
    | Project A | 40,000 |
    | Project B | 40,000 |
    | Project C | 20,000 |

    Then, A and & are mutually exclusive projects as doing A will prohibit doing B, but A & C or B & C are independent projects.

!!! Note "Some other terms"

    ==Normal Cash Flow Stream==: Cost(negative CF) followed by a series of positive cash inflows. One change in sign of cash flow.

    ==Non-normal Cash Flow Stream==: Two or more changes in the sign of cash flows.

## An example
> A company is considering an investment proposal to install new milling controls. The project will cost ^^Rs.80,000^^. The facility has a life expectancy of ^^5 years^^ and no ^^salvage value^^. The company’s ^^tax rate is 40%^^ and ^^no investment allowance is allowed^^. The firm uses ^^straight line depreciation^^. The estimated earnings before tax (EBT) from the proposed investment proposal are as follows:  

> | Year | 1 | 2 | 3 | 4 | 5 |
> |------|---|---|---|---|---|
> | EBT | 10,000 | 11,000 | 14,000 | 15,000 | 25,000 |

> Calculate the following for the project:

> - Payback period
> - Discounted Pay back period
> - NPV at 10% discount rate (weighted average cost of capital)
> - Profitability index at 10% discount rate
> - IRR (Internal Rate of return)
> - Average Accounting Rate of Return
> - Modified IRR (MIRR) using 10% reinvestment rate (Terminal Value Method – TVM) 

| Year | 1 | 2 | 3 | 4 | 5 |
|------|---|---|---|---|---|
| EBT | 10,000 | 11,000 | 14,000 | 15,000 | 25,000 |
| Tax | 4,000 | 4,400 | 5,600 | 6,000 | 10,000 |
| EAT | 6,000 | 6,600 | 8,400 | 9,000 | 15,000 |

### Accounting Rate of Return(ARR)

$$\text{ARR} = \frac{\text{Average Annual Profit}}{\text{Average Investment}}$$

If ARR $\geq$ Required rate of return, then the project is acceptable, else reject.

$$
\begin{align*}
\text{Average Net Profit/EAT} &= \frac{6000+6600+8400+9000+15000}{5} = 9000 \\
\text{Average Investment} &= \frac{\text{Beginning Value} + \text{Ending Value}}{2} = \frac{80,000 + 0}{2} = 40,000 \\
\text{ARR} &= \frac{9000}{40000} = 0.225 = 22.5\%
\end{align*}
$$

### Payback Period

Now, Company uses straight-line depreciation, so depreciation per year is $80,000/5 = 16,000$

| Year | 1 | 2 | 3 | 4 | 5 |
|------|---|---|---|---|---|
| EAT | 6,000 | 6,600 | 8,400 | 9,000 | 15,000 |
| Depreciation | 16,000 | 16,000 | 16,000 | 16,000 | 16,000 |
| Cash Flow after Tax(CFAT)(EAT + Depreciation) | 22,000 | 22,600 | 24,400 | 25,000 | 31,000 |
| Cumulative CFAT | 22,000 | 44,600 | ^^69,000^^ | ^^94,000^^ | 125,000 |

Our Cumulative is reached between year 3 and 4, therefore payback period is 

$$\text{Payback Period} = 3 + \frac{80,000 - 69,000}{94,000 - 69,000} = 3.44 \text{years}$$

The lower the payback period, the better the project.

### Discounted Payback Period

Now we know that the discount rate is 10%, so we will discount the cash flows to present value.

| Year | 1 | 2 | 3 | 4 | 5 |
|------|---|---|---|---|---|
| CFAT | 22,000 | 22,600 | 24,400 | 25,000 | 31,000 |
| Discounted CFAT | $\frac{20,000}{1.10}$ | $\frac{22,600}{1.10^2}$ | $\frac{24,400}{1.10^3}$ | $\frac{25,000}{1.10^4}$ | $\frac{31,000}{1.10^5}$ |
| Discounted CFAT | 20,000 | 18,678 | 18,332 | 17,075 | 19,249 |
| Cumulative Discounted CFAT | 20,000 | 38,678 | 57,010 | 74,085 | 93,364 |

The Cumulative Discounted CFAT is reached between year 4 and 5, therefore discounted payback period is

$$\text{Discounted Payback Period} = 4 + \frac{80,000 - 74,085}{93,364 - 74,085} = 4.31 \text{years}$$

### Net Present Value or NPV

$$
\begin{align*}
\text{NPV} &= \sum \frac{CFAT}{(1+r)^t} - \text{Initial Investment} \\
&= 93,364 - 80,000 = 13,364
\end{align*}
$$

Since NPV is positive, the project is acceptable.

### Profitability Index

Very similar to net present value. If PI > 1, then the project is acceptable.

$$\text{PI} = \frac{PV of Inflows}{PV of Outflows} = \frac{93,364}{80,000} = 1.167$$

### Internal Rate of Return(IRR)

IRR is the discount rate that forces PV of inflows equal to cost, and the NPV is zero.

$$
\begin{align*}
0 &= \sum_{t = 1}^{n} \frac{CF_t}{(1+IRR)^t} - CF_0 \\
80,000 &= \frac{22,600}{(1+IRR)^1} + \frac{24,400}{(1+IRR)^2} + \frac{25,000}{(1+IRR)^3} + \frac{31,000}{(1+IRR)^4} \\
\end{align*}
$$

The rate comes out to be around 16%. But calculating it manually is a tedious task, so we use excel or financial calculators, or the following approximation

$$\text{IRR} = r_{\text{lower}} + \frac{NPV_{\text{lower}}}{NPV_{\text{lower}} - NPV_{\text{upper}}} \times (r_{\text{upper}} - r_{\text{lower}})$$

Where $r_{\text{lower}}$ and $r_{\text{upper}}$ are the discount rates that give NPV of -ve and +ve respectively, and $NPV_{\text{lower}}$ and $NPV_{\text{upper}}$ are the NPVs at those rates. The closer the NPVs are to 0, better the approximation.


## NPV vs IRR

There can be multiple values of IRR for non-normal NPV. Which one to choose? There is also a size problem with IRR.

| Time | 0 | 1 | 2 | NPV(10%) | IRR |
|------|---|---|---|----------|-----|
| Project A | -10 | 10 | 20 | 25.62 | 100% |
| Project B | -10,000 | 10,000 | 20,000 | 25,620 | 100% |

There is also a timing problem with IRR

| Time | 0 | 1 | 2 | NPV(10%) | IRR |
|------|---|---|---|----------|-----|
| Project A | -1000 | 1,150 | 100 | 128 | 23% |
| Project B | -1000 | 100 | 1300 | 165.3 | 19% |

Sometimes there is a conflict between the decision based on NPV and IRR methods. This is caused due to underlying reinvestment rate assumption 

- NPV assumes cash flows are reinvested at the required rate, $k$ or $r$
- IRR assumes cash flows are reinvested at the IRR

Out of these two, the first is more realistic, as most projects earn approximately $k$. Therefore, NPV is preferred over IRR.

## Modified IRR(MIRR)

| 0 | 1 | 2 |
|---|---|---|
| -800,000 | 5,000,000 | -5,000,000 |

PV outflows at 10% = $800,000 + 5,000,000/(1.10)^2 = 4932231.40496$
TV of inflows at 10% = 5,000,000 * 1.10 = 5,500,000

$$\text{MIRR} = \left( \frac{5,500,000}{4932231.40496} \right)^{1/2} - 1 = 0.056 = 5.6\%$$

Since MIRR is less than the required rate of return, the project is rejected.


