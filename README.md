# Credit Risk Modelling

**An AI-assisted quantitative finance project for estimating credit losses using PD, LGD, and EAD models.**

[![Python 3.14+](https://img.shields.io/badge/Python-3.14%2B-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?logo=jupyter&logoColor=white)](https://jupyter.org/)
[![AI Assisted](https://img.shields.io/badge/AI-Assisted%20SDLC-blueviolet?logo=google&logoColor=white)](#6-ai-assisted-development)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

---

*Built with an AI-assisted software development lifecycle. Every commit, review, and documentation pass is human-guided and AI-augmented.*

</div>

## Contents

- [1. Overview](#1-overview)
- [2. Credit risk fundamentals](#2-credit-risk-fundamentals)
  - [2.1 Loan application flow](#21-loan-application-flow)
  - [2.2 Assessing creditworthiness](#22-assessing-creditworthiness)
- [3. Regulatory and accounting frameworks](#3-regulatory-and-accounting-frameworks)
  - [3.1 Three pillars of Basel](#31-three-pillars-of-basel)
  - [3.2 Minimum capital requirement](#32-minimum-capital-requirement)
  - [3.3 Expected and unexpected loss](#33-expected-and-unexpected-loss)
- [4. Expected credit loss (ECL)](#4-expected-credit-loss-ecl)
  - [4.1 ECL components](#41-ecl-components)
  - [4.2 A simple ECL calculation](#42-a-simple-ecl-calculation)
  - [4.3 Scenario weighting and discounting](#43-scenario-weighting-and-discounting)
  - [4.4 IFRS 9 stages](#44-ifrs-9-stages)
  - [4.5 ECL allowance](#45-ecl-allowance)
- [5. Capital adequacy and credit risk models](#5-capital-adequacy-and-credit-risk-models)
  - [5.1 Capital adequacy ratio (CAR)](#51-capital-adequacy-ratio-car)
  - [5.2 Approaches to estimating risk parameters](#52-approaches-to-estimating-risk-parameters)
  - [5.3 Credit scores, ratings, and model inputs](#53-credit-scores-ratings-and-model-inputs)
- [6. Model specification](#6-model-specification)
  - [6.1 Probability of default (PD) model](#61-probability-of-default-pd-model)
  - [6.2 Loss given default (LGD) model](#62-loss-given-default-lgd-model)
  - [6.3 Exposure at default (EAD) model](#63-exposure-at-default-ead-model)
- [7. Project structure](#7-project-structure)
- [8. Getting started](#8-getting-started)
- [9. AI-assisted development](#9-ai-assisted-development)
- [10. Contributing](#10-contributing)
- [11. License](#11-license)

---

## 1. Overview

This project explores credit risk modelling from first principles through working code. It covers the theory behind expected credit losses, walks through the Basel and IFRS 9 frameworks, and implements a data analysis pipeline on a LendingClub loan dataset (2,000 records, 74 features).

```mermaid
graph LR
    subgraph Data
        A[Loan Dataset<br/>2,000 rows x 74 cols]
    end
    subgraph Pipeline
        B[Data Loading &<br/>Exploration]
        C[Feature<br/>Engineering]
        D[PD Model]
        E[LGD Model]
        F[EAD Model]
    end
    subgraph Output
        G[ECL<br/>Estimates]
    end
    A --> B --> C --> D & E & F --> G
```

**Key goals:**

1. Document credit risk concepts in plain language with worked examples.
2. Build PD, LGD, and EAD estimation pipelines on real loan data.
3. Demonstrate an AI-assisted SDLC workflow where every stage is human-guided and AI-augmented.

---

## 2. Credit risk fundamentals

### 2.1 Loan application flow

```mermaid
flowchart LR
    Customer -->|Applies for a loan| Bank
    Bank -->|Accepts or rejects| Customer
```

Credit risk is the possibility that a borrower will not repay a loan as agreed. The repayment obligation includes both principal and interest. Banks consider this risk when deciding whether to approve a loan.

### 2.2 Assessing creditworthiness

Creditworthiness is commonly assessed using the **5 C's**. Together, they help describe a borrower's reliability, ability to repay, financial resources, circumstances, and available security:

| Factor | Description |
| --- | --- |
| **Character** | The borrower's history of meeting financial obligations and willingness to repay. |
| **Capacity** | The borrower's ability to make repayments from income or cash flow. |
| **Capital** | The borrower's own financial resources or investment. |
| **Condition** | Circumstances that may affect repayment, such as the loan's purpose or relevant economic conditions. |
| **Collateral** | An asset pledged to secure the loan, which may help limit the lender's loss if the borrower defaults. |

---

## 3. Regulatory and accounting frameworks

The **Basel framework** sets international prudential standards for banks. Local regulators, such as the Reserve Bank of India (RBI), implement requirements in their jurisdictions. **IFRS** (International Financial Reporting Standards) is a separate set of financial reporting standards; IFRS 9 includes requirements for recognizing expected credit losses. Basel governs how much capital banks must hold; IFRS 9 governs how banks report credit losses in their financial statements.

### 3.1 Three pillars of Basel

The Basel framework is commonly described through three pillars:

| Pillar | Purpose |
| --- | --- |
| 1. Minimum capital requirement | Set minimum capital banks must hold to absorb losses. |
| 2. Supervisory review | Allow supervisors to review a bank's capital adequacy and risk management. |
| 3. Market discipline | Encourage transparency so market participants can assess a bank's risk and capital position. |

Basel I, II, and III are successive versions of the Basel framework.

### 3.2 Minimum capital requirement

For the first pillar, banks calculate required capital using an approach permitted by their regulator:

- **Standardized Approach (SA):** Uses regulator-defined rules and risk weights.
- **Internal Ratings-Based (IRB) Approach:** Uses a bank's internal risk estimates, subject to regulatory approval. It has Foundation (FIRB) and Advanced (AIRB) forms.

### 3.3 Expected and unexpected loss

Credit risk analysis distinguishes expected loss from unexpected loss:

- **Expected credit loss (ECL)** is the estimated average loss over a specified period. A simplified calculation is:

  `ECL = PD x LGD x EAD`

  - **PD** - Probability of default
  - **LGD** - Loss given default
  - **EAD** - Exposure at default
- **Unexpected loss (UL)** is loss beyond the expected level. Banks generally hold capital to help absorb unexpected losses.

---

## 4. Expected credit loss (ECL)

Expected credit loss is an estimate of the credit losses a bank expects over a specified period. It is forward-looking and may change as borrower risk, expected recoveries, and economic conditions change. ECL is an estimate, not a prediction of the exact amount that will be lost.

### 4.1 ECL components

A simplified, single-period estimate is:

`ECL = PD x LGD x EAD`

The three inputs describe different parts of the risk:

- **Probability of default (PD)** is the likelihood that the borrower will default over a specified period. A simple historical estimate is the number of defaults divided by the number of comparable borrowers observed. For example, 50 defaults among 1,000 borrowers gives a historical rate of 5%. A practical estimate may also account for borrower characteristics, the economic outlook, and the model's time horizon.
- **Loss given default (LGD)** is the percentage of exposure expected to be lost if default occurs, after recoveries. In a simplified calculation, `LGD = (EAD - expected recoveries) / EAD`. For an EAD of 10 lakh and expected recoveries of 4 lakh, LGD is 60%. Collateral may increase recoveries and reduce LGD.
- **Exposure at default (EAD)** is the amount expected to be owed when default occurs. For a fully drawn loan, it may be close to the outstanding balance. For a revolving facility, it can include expected additional borrowing before default. For example, 6 lakh drawn plus an estimated 50% of a remaining 4 lakh limit gives an EAD of 8 lakh.

### 4.2 A simple ECL calculation

Suppose a loan has an EAD of 10 lakh, a PD of 2%, and an LGD of 60%:

`ECL = 0.02 x 0.60 x 10,00,000 = 12,000`

The loss if default occurs is 6 lakh (60% of the EAD), while 12,000 is the simplified expected loss before the outcome is known. It is an estimate, not a guarantee of the actual loss.

### 4.3 Scenario weighting and discounting

Actual accounting ECL is more involved than the single-period formula. Under IFRS 9, it is a probability-weighted estimate of the present value of expected cash shortfalls. This means the estimate considers multiple reasonable future economic scenarios and the timing of expected payments and recoveries.

For example, assume a 10 lakh exposure and ignore discounting:

| Scenario | Scenario probability | PD | LGD | Scenario ECL |
| --- | ---: | ---: | ---: | ---: |
| Good economy | 30% | 1% | 40% | 4,000 |
| Base case | 50% | 2% | 50% | 10,000 |
| Recession | 20% | 8% | 70% | 56,000 |

Weighting each scenario's ECL by its probability gives:

`ECL = (30% x 4,000) + (50% x 10,000) + (20% x 56,000) = 17,400`

Discounting reflects that a future cash shortfall is not equivalent to the same amount lost today. IFRS 9 generally uses the original effective interest rate, subject to applicable exceptions. Scenario values and probabilities in this example are illustrative.

### 4.4 IFRS 9 stages

The recognized ECL depends on how credit risk has changed since the loan was first recognized:

| Stage | Credit status | ECL recognized |
| --- | --- | --- |
| 1 | No significant increase in credit risk since initial recognition | 12-month ECL |
| 2 | Significant increase in credit risk, but not credit-impaired | Lifetime ECL |
| 3 | Credit-impaired | Lifetime ECL |

12-month ECL covers losses arising from default events that could occur in the next 12 months over the life of the instrument. It does not mean that only cash losses occurring within those 12 months are counted. Lifetime ECL considers possible default events over the remaining life of the instrument.

A loan can move from Stage 1 to Stage 2 when credit risk has increased significantly, even before a missed payment. If it later becomes credit-impaired, it moves to Stage 3. The treatment of interest income also changes for Stage 3 assets.

### 4.5 ECL allowance

The ECL allowance, also called a loss allowance, is the amount recognized for estimated credit losses under the applicable accounting rules. It is not necessarily cash held in a separate account. Recognizing or increasing the allowance generally reduces reported profit, all else equal.

The allowance is not the actual loss ultimately realized. It can change as borrower risk, economic forecasts, and expected recoveries change.

---

## 5. Capital adequacy and credit risk models

Banks fund assets such as loans through liabilities, such as deposits, and equity capital. Regulatory capital requirements help ensure a bank can absorb losses and continue operating.

### 5.1 Capital adequacy ratio (CAR)

The capital adequacy ratio (CAR), also called the capital-to-risk-weighted-assets ratio, compares a bank's regulatory capital with its risk-weighted assets (RWA):

`CAR = Regulatory capital / Risk-weighted assets x 100%`

Loans are among a bank's assets, and their contribution to RWA depends on their risk treatment. Basel sets international standards, while local regulators set and apply requirements. The often-quoted 8% is a Basel minimum total capital ratio, not a universal complete requirement for every bank: applicable buffers and local rules can require more.

### 5.2 Approaches to estimating risk parameters

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

### 5.3 Credit scores, ratings, and model inputs

Individual credit scores and entity credit ratings are related but distinct:

- **Credit scores** summarize an individual's credit history. Examples include FICO scores, commonly reported on a 300 to 850 scale, and credit bureau scores such as CIBIL scores in India.
- **Credit ratings** such as S&P Global Ratings' AAA, AA, and BBB categories generally assess the creditworthiness of entities or debt instruments, rather than providing an individual's bureau score.

Credit risk models may use relevant borrower and facility information, such as repayment and enquiry history, income, credit bureau data, loan type, and collateral. Variables must be selected and governed according to applicable law and model-risk policies.

For a mortgage, loan-to-value (LTV) compares the loan balance with the property's value:

`LTV = Loan balance / Property value x 100%`

For example, a 40 lakh loan against a property valued at 50 lakh has an LTV of 80%. LTV can change as the loan is repaid or the property value changes.

Statistical methods depend on the target and data. Logistic regression is commonly used to estimate PD. Beta regression can be suitable for bounded LGD rates, while EAD methods depend on the product and target definition. No single model type is required for every portfolio.

---

## 6. Model specification

A credit risk model uses a **dependent variable**, also called the target, to represent the outcome it estimates. **Independent variables**, also called predictors or features, are information used by the model to estimate that outcome. Inputs should be relevant to the prediction date and available when the estimate is made.

### 6.1 Probability of default (PD) model

A PD model estimates the likelihood that a borrower will default within a defined period, such as 12 months.

- **Target:** A binary outcome, commonly coded `1` for default and `0` for no default during the defined period.
- **Possible predictors:** Borrower characteristics such as income, employment, and credit history; loan features such as amount, interest rate, and term; behavior such as missed payments, credit utilization, and recent credit enquiries; and macroeconomic indicators such as GDP growth, inflation, and unemployment.

### 6.2 Loss given default (LGD) model

An LGD model estimates the proportion of exposure expected to be lost if default occurs, after recoveries.

- **Target:** A loss rate, commonly represented between 0 and 1 or as a percentage from 0% to 100%. A simplified definition is `LGD = loss after recoveries / EAD`.
- **Possible predictors:** Collateral type and loan-to-value ratio; loan amount and whether it is secured; borrower credit score and financial condition; and relevant conditions such as property market trends and recovery experience.

### 6.3 Exposure at default (EAD) model

An EAD model estimates the amount the bank is exposed to when default occurs.

- **Target:** A monetary amount representing exposure at the point of default.
- **Possible predictors:** Credit limit, current utilization, and loan or facility type; borrower usage and repayment behavior; and relevant macroeconomic conditions, such as interest rate trends or an economic downturn.

The target definition and prediction horizon should be set consistently for each portfolio. Predictors should be checked for data quality, relevance, and availability at the time the model is intended to make its prediction.

---

## 7. Project structure

```
credit-risk-modelling/
├── AGENTS.md               # AI agent instructions and project rules
├── README.md               # This file
├── LICENSE                  # MIT License
├── .gitignore               # Git ignore rules
├── requirements.txt         # Python dependencies
├── data/
│   └── loan_data.csv        # LendingClub loan dataset (2,000 records, 74 features)
└── main.ipynb               # Primary analysis notebook
```

---

## 8. Getting started

### Prerequisites

- Python 3.14 or higher
- pip or a compatible package manager

### Setup

```bash
# 1. Clone the repository
git clone https://github.com/Prayag2003/credit-risk-modelling.git
cd credit-risk-modelling

# 2. Create and activate a virtual environment
python -m venv .venv
source .venv/bin/activate        # macOS / Linux
# .venv\Scripts\activate         # Windows

# 3. Install dependencies
pip install -r requirements.txt

# 4. Launch the notebook
jupyter notebook main.ipynb
```

### Dataset

The dataset (`data/loan_data.csv`) contains 2,000 anonymized LendingClub loan records with 74 features covering:

| Category | Example columns |
| --- | --- |
| Loan attributes | `loan_amnt`, `funded_amnt`, `term`, `int_rate`, `installment`, `grade` |
| Borrower profile | `annual_inc`, `emp_length`, `home_ownership`, `dti` |
| Credit history | `delinq_2yrs`, `earliest_cr_line`, `inq_last_6mths`, `revol_util` |
| Repayment data | `loan_status`, `total_pymnt`, `recoveries`, `last_pymnt_amnt` |

---

## 9. AI-assisted development

This project follows an **AI-assisted SDLC** model. Every stage of development is human-guided and AI-augmented:

```mermaid
flowchart TB
    subgraph Planning
        A[Requirements<br/>& Research]
        B[Architecture<br/>Design]
    end
    subgraph Development
        C[Code<br/>Generation]
        D[Code<br/>Review]
    end
    subgraph Quality
        E[Documentation<br/>& Testing]
        F[Continuous<br/>Improvement]
    end

    A --> B --> C --> D --> E --> F
    F -.->|Feedback loop| A

    style A fill:#4A90D9,color:#fff
    style B fill:#4A90D9,color:#fff
    style C fill:#7B68EE,color:#fff
    style D fill:#7B68EE,color:#fff
    style E fill:#2ECC71,color:#fff
    style F fill:#2ECC71,color:#fff
```

| SDLC Phase | Human Role | AI Role |
| --- | --- | --- |
| **Planning** | Define scope, choose frameworks, set constraints | Research regulatory details, draft initial specs |
| **Development** | Review, validate, and merge code | Generate boilerplate, suggest implementations |
| **Documentation** | Set structure, verify accuracy | Draft content, format tables and diagrams |
| **Review** | Final approval, domain validation | Flag inconsistencies, suggest improvements |
| **Testing** | Design test strategy, interpret results | Generate test cases, run validation checks |

### Principles

1. **Human-in-the-loop always.** AI generates drafts; humans validate, correct, and approve.
2. **Transparency.** AI-generated content is reviewed for factual accuracy, especially for regulatory and financial concepts.
3. **Reproducibility.** All code, data, and instructions are version-controlled so any result can be independently verified.
4. **Iterative refinement.** The project evolves through cycles of AI-assisted drafting and human-guided correction, captured in commit history.

---

## 10. Contributing

Contributions are welcome. Please follow these guidelines:

1. **Fork** the repository and create a feature branch from `main`.
2. Follow the conventions in [`AGENTS.md`](AGENTS.md) for documentation style.
3. Keep commits focused and use descriptive messages (see the existing commit history for style).
4. Open a pull request with a clear description of what changed and why.

---

## 11. License

This project is licensed under the [MIT License](LICENSE).

---

<div align="center">
<sub>Built with curiosity, quantitative rigor, and AI-assisted development.</sub>
</div>
