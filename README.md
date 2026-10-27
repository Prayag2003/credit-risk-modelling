# Credit Risk Modelling

## Contents

- [1. What is credit risk?](#1-what-is-credit-risk)
  - [1.1 Loan application flow](#11-loan-application-flow)
  - [1.2 Assessing creditworthiness](#12-assessing-creditworthiness)
- [2. Three pillars of credit risk management](#2-three-pillars-of-credit-risk-management)
  - [2.1 Minimum capital requirement](#21-minimum-capital-requirement)
  - [2.2 Expected and unexpected loss](#22-expected-and-unexpected-loss)
- [3. Expected credit loss (ECL)](#3-expected-credit-loss-ecl)
  - [3.1 ECL components](#31-ecl-components)
  - [3.2 A simple ECL calculation](#32-a-simple-ecl-calculation)
  - [3.3 Scenario weighting and discounting](#33-scenario-weighting-and-discounting)
  - [3.4 IFRS 9 stages](#34-ifrs-9-stages)
  - [3.5 ECL allowance](#35-ecl-allowance)
- [4. Capital adequacy and credit risk models](#4-capital-adequacy-and-credit-risk-models)
  - [4.1 Capital adequacy ratio (CAR)](#41-capital-adequacy-ratio-car)
  - [4.2 Approaches to estimating risk parameters](#42-approaches-to-estimating-risk-parameters)
  - [4.3 Credit scores, ratings, and model inputs](#43-credit-scores-ratings-and-model-inputs)
- [5. Dependent and independent variables](#5-dependent-and-independent-variables)
  - [5.1 Probability of default (PD) model](#51-probability-of-default-pd-model)
  - [5.2 Loss given default (LGD) model](#52-loss-given-default-lgd-model)
  - [5.3 Exposure at default (EAD) model](#53-exposure-at-default-ead-model)

## 1. What is credit risk?

### 1.1 Loan application flow

```mermaid
flowchart LR
    Customer -->|Applies for a loan| Bank
    Bank -->|Accepts or rejects| Customer
```

Credit risk is the possibility that a borrower will not repay a loan as agreed. The repayment obligation includes both principal and interest. Banks consider this risk when deciding whether to approve a loan.

### 1.2 Assessing creditworthiness

Creditworthiness is commonly assessed using the 5 C's. Together, they help describe a borrower's reliability, ability to repay, financial resources, circumstances, and available security:

- **Character:** The borrower's history of meeting financial obligations and willingness to repay.
- **Capacity:** The borrower's ability to make repayments from income or cash flow.
- **Capital:** The borrower's own financial resources or investment.
- **Condition:** Circumstances that may affect repayment, such as the loan's purpose or relevant economic conditions.
- **Collateral:** An asset pledged to secure the loan, which may help limit the lender's loss if the borrower defaults.

## 2. Three pillars of credit risk management

The Basel framework sets international prudential standards for banks. Local regulators, such as the Reserve Bank of India (RBI), implement requirements in their jurisdictions. IFRS is a separate set of financial reporting standards; IFRS 9 includes requirements for recognizing expected credit losses.

The Basel framework is commonly described through three pillars:

| Pillar | Purpose |
| --- | --- |
| 1. Minimum capital requirement | Set minimum capital banks must hold to absorb losses. |
| 2. Supervisory review | Allow supervisors to review a bank's capital adequacy and risk management. |
| 3. Market discipline | Encourage transparency so market participants can assess a bank's risk and capital position. |

Basel I, II, and III are successive versions of the Basel framework.

### 2.1 Minimum capital requirement

For the first pillar, banks calculate required capital using an approach permitted by their regulator:

- **Standardized Approach (SA):** Uses regulator-defined rules and risk weights.
- **Internal Ratings-Based (IRB) Approach:** Uses a bank's internal risk estimates, subject to regulatory approval. It has Foundation (FIRB) and Advanced (AIRB) forms.

### 2.2 Expected and unexpected loss

Credit risk analysis distinguishes expected loss from unexpected loss:

- **Expected credit loss (ECL)** is the estimated average loss over a specified period. A simplified calculation is:

  `ECL = PD × LGD × EAD`

  - **PD:** Probability of default
  - **LGD:** Loss given default
  - **EAD:** Exposure at default
- **Unexpected loss (UL)** is loss beyond the expected level. Banks generally hold capital to help absorb unexpected losses.

## 3. Expected credit loss (ECL)

Expected credit loss is an estimate of the credit losses a bank expects over a specified period. It is forward-looking and may change as borrower risk, expected recoveries, and economic conditions change. ECL is an estimate, not a prediction of the exact amount that will be lost.

### 3.1 ECL components

A simplified, single-period estimate is:

`ECL = PD × LGD × EAD`

The three inputs describe different parts of the risk:

- **Probability of default (PD)** is the likelihood that the borrower will default over a specified period. A simple historical estimate is the number of defaults divided by the number of comparable borrowers observed. For example, 50 defaults among 1,000 borrowers gives a historical rate of 5%. A practical estimate may also account for borrower characteristics, the economic outlook, and the model's time horizon.
- **Loss given default (LGD)** is the percentage of exposure expected to be lost if default occurs, after recoveries. In a simplified calculation, `LGD = (EAD - expected recoveries) / EAD`. For an EAD of ₹10 lakh and expected recoveries of ₹4 lakh, LGD is 60%. Collateral may increase recoveries and reduce LGD.
- **Exposure at default (EAD)** is the amount expected to be owed when default occurs. For a fully drawn loan, it may be close to the outstanding balance. For a revolving facility, it can include expected additional borrowing before default. For example, ₹6 lakh drawn plus an estimated 50% of a remaining ₹4 lakh limit gives an EAD of ₹8 lakh.

### 3.2 A simple ECL calculation

Suppose a loan has an EAD of ₹10 lakh, a PD of 2%, and an LGD of 60%:

`ECL = 0.02 × 0.60 × ₹10,00,000 = ₹12,000`

The loss if default occurs is ₹6 lakh (60% of the EAD), while ₹12,000 is the simplified expected loss before the outcome is known. It is an estimate, not a guarantee of the actual loss.

### 3.3 Scenario weighting and discounting

Actual accounting ECL is more involved than the single-period formula. Under IFRS 9, it is a probability-weighted estimate of the present value of expected cash shortfalls. This means the estimate considers multiple reasonable future economic scenarios and the timing of expected payments and recoveries.

For example, assume a ₹10 lakh exposure and ignore discounting:

| Scenario | Scenario probability | PD | LGD | Scenario ECL |
| --- | ---: | ---: | ---: | ---: |
| Good economy | 30% | 1% | 40% | ₹4,000 |
| Base case | 50% | 2% | 50% | ₹10,000 |
| Recession | 20% | 8% | 70% | ₹56,000 |

Weighting each scenario's ECL by its probability gives:

`ECL = (30% × ₹4,000) + (50% × ₹10,000) + (20% × ₹56,000) = ₹17,400`

Discounting reflects that a future cash shortfall is not equivalent to the same amount lost today. IFRS 9 generally uses the original effective interest rate, subject to applicable exceptions. Scenario values and probabilities in this example are illustrative.

### 3.4 IFRS 9 stages

The recognized ECL depends on how credit risk has changed since the loan was first recognized:

| Stage | Credit status | ECL recognized |
| --- | --- | --- |
| 1 | No significant increase in credit risk since initial recognition | 12-month ECL |
| 2 | Significant increase in credit risk, but not credit-impaired | Lifetime ECL |
| 3 | Credit-impaired | Lifetime ECL |

12-month ECL covers losses arising from default events that could occur in the next 12 months over the life of the instrument. It does not mean that only cash losses occurring within those 12 months are counted. Lifetime ECL considers possible default events over the remaining life of the instrument.

A loan can move from Stage 1 to Stage 2 when credit risk has increased significantly, even before a missed payment. If it later becomes credit-impaired, it moves to Stage 3. The treatment of interest income also changes for Stage 3 assets.

### 3.5 ECL allowance

The ECL allowance, also called a loss allowance, is the amount recognized for estimated credit losses under the applicable accounting rules. It is not necessarily cash held in a separate account. Recognizing or increasing the allowance generally reduces reported profit, all else equal.

The allowance is not the actual loss ultimately realized. It can change as borrower risk, economic forecasts, and expected recoveries change.

## 4. Capital adequacy and credit risk models

Banks fund assets such as loans through liabilities, such as deposits, and equity capital. Regulatory capital requirements help ensure a bank can absorb losses and continue operating.

### 4.1 Capital adequacy ratio (CAR)

The capital adequacy ratio (CAR), also called the capital-to-risk-weighted-assets ratio, compares a bank's regulatory capital with its risk-weighted assets (RWA):

`CAR = Regulatory capital / Risk-weighted assets × 100%`

Loans are among a bank's assets, and their contribution to RWA depends on their risk treatment. Basel sets international standards, while local regulators set and apply requirements. The often-quoted 8% is a Basel minimum total capital ratio, not a universal complete requirement for every bank: applicable buffers and local rules can require more.

### 4.2 Approaches to estimating risk parameters

Compare the approaches by which party determines each risk input:

| Risk input | Standardized Approach (SA) | Foundation IRB (FIRB) | Advanced IRB (AIRB) |
| --- | --- | --- | --- |
| Probability of default (PD) | Regulatory rules | Bank estimate | Bank estimate |
| Loss given default (LGD) | Regulatory rules | Generally supervisory values | Bank estimate |
| Exposure at default (EAD) | Regulatory rules | Generally supervisory values | Bank estimate |
| Risk weights | Set by regulatory rules | Calculated using approved IRB parameters | Calculated using approved IRB parameters |

<details>
<summary>What do the approaches mean?</summary>

- **SA:** Applies regulator-defined rules and risk weights.
- **FIRB:** The bank estimates PD, while supervisory values generally apply to LGD and EAD.
- **AIRB:** The bank estimates PD, LGD, and EAD, subject to regulatory approval and requirements.

</details>

The precise requirements and permitted use of estimates depend on the applicable Basel rules and local regulator. Internal approaches are not simply a way for banks to lend more; they require regulatory approval and controls.

### 4.3 Credit scores, ratings, and model inputs

Individual credit scores and entity credit ratings are related but distinct:

- **Credit scores** summarize an individual's credit history. Examples include FICO scores, commonly reported on a 300 to 850 scale, and credit bureau scores such as CIBIL scores in India.
- **Credit ratings** such as S&P Global Ratings' AAA, AA, and BBB categories generally assess the creditworthiness of entities or debt instruments, rather than providing an individual's bureau score.

Credit risk models may use relevant borrower and facility information, such as repayment and enquiry history, income, credit bureau data, loan type, and collateral. Variables must be selected and governed according to applicable law and model-risk policies.

For a mortgage, loan-to-value (LTV) compares the loan balance with the property's value:

`LTV = Loan balance / Property value × 100%`

For example, a ₹40 lakh loan against a property valued at ₹50 lakh has an LTV of 80%. LTV can change as the loan is repaid or the property value changes.

Statistical methods depend on the target and data. Logistic regression is commonly used to estimate PD. Beta regression can be suitable for bounded LGD rates, while EAD methods depend on the product and target definition. No single model type is required for every portfolio.

## 5. Dependent and independent variables

A credit risk model uses a **dependent variable**, also called the target, to represent the outcome it estimates. **Independent variables**, also called predictors or features, are information used by the model to estimate that outcome. Inputs should be relevant to the prediction date and available when the estimate is made.

### 5.1 Probability of default (PD) model

A PD model estimates the likelihood that a borrower will default within a defined period, such as 12 months.

- **Target:** A binary outcome, commonly coded `1` for default and `0` for no default during the defined period.
- **Possible predictors:** Borrower characteristics such as income, employment, and credit history; loan features such as amount, interest rate, and term; behavior such as missed payments, credit utilization, and recent credit enquiries; and macroeconomic indicators such as GDP growth, inflation, and unemployment.

### 5.2 Loss given default (LGD) model

An LGD model estimates the proportion of exposure expected to be lost if default occurs, after recoveries.

- **Target:** A loss rate, commonly represented between 0 and 1 or as a percentage from 0% to 100%. A simplified definition is `LGD = loss after recoveries / EAD`.
- **Possible predictors:** Collateral type and loan-to-value ratio; loan amount and whether it is secured; borrower credit score and financial condition; and relevant conditions such as property market trends and recovery experience.

### 5.3 Exposure at default (EAD) model

An EAD model estimates the amount the bank is exposed to when default occurs.

- **Target:** A monetary amount representing exposure at the point of default.
- **Possible predictors:** Credit limit, current utilization, and loan or facility type; borrower usage and repayment behavior; and relevant macroeconomic conditions, such as interest rate trends or an economic downturn.

The target definition and prediction horizon should be set consistently for each portfolio. Predictors should be checked for data quality, relevance, and availability at the time the model is intended to make its prediction.
