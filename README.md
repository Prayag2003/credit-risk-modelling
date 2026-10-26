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
