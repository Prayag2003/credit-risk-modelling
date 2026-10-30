<![CDATA[# Project Instructions

## Documentation Rules

1. Keep credit-risk documentation concise, clearly structured, and numbered consistently with the README contents links.
2. Explain concepts in plain language and define abbreviations on first use (e.g., PD = Probability of default).
3. Distinguish the Basel prudential framework from IFRS financial reporting standards; do not describe either as belonging to only one region.
4. When documenting loss estimates, define PD, LGD, and EAD and identify simplified formulas as such.
5. Add only information relevant to credit risk modelling, and correct factual inaccuracies rather than repeating them.
6. Do not use em-dashes in any content. Use commas, semicolons, or rewrite the sentence instead.

## Code Standards

7. Use Python 3.14+ features and idioms. Type hints are encouraged for all function signatures.
8. Follow PEP 8 style. Maximum line length is 100 characters.
9. All data paths must be relative to the project root (e.g., `data/loan_data.csv`), never absolute paths.
10. Notebook cells should be ordered logically: imports, configuration, data loading, exploration, feature engineering, modelling, evaluation.
11. Add a brief markdown cell before each code section explaining what it does and why.

## Data Handling

12. Never commit raw customer data or PII. The dataset in `data/` uses anonymized LendingClub records.
13. Use pandas for data manipulation. Keep transformations reproducible and clearly commented.
14. Document any assumptions about missing values, outliers, or data quality in markdown cells or code comments.

## AI-Assisted Development

15. AI-generated content (code, documentation, formulas) must be reviewed by a human before merging.
16. Regulatory and financial claims must be verified against primary sources (Basel Committee publications, IFRS Foundation standards).
17. Commit messages should be descriptive and follow the existing convention: `[scope]: description`.
18. When AI suggests a code change, validate it against the dataset and existing pipeline before accepting.

## Model Development

19. Clearly separate data preparation, model training, and evaluation stages.
20. Document model assumptions, limitations, and the rationale for choosing a specific approach.
21. Use reproducible random seeds where randomness is involved.
22. Log model performance metrics and include them in notebook outputs.
]]>