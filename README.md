# Credit Risk & Borrower Default Analytics Dashboard

An executive-level Power BI dashboard designed to analyze loan portfolio defaults, isolate high-risk borrower segments, and evaluate key financial exposure metrics.

<img width="991" height="738" alt="Screenshot 2026-07-18 160551" src="https://github.com/user-attachments/assets/64e3342d-34ac-4882-8619-6fadbf229576" />

## Key Features & Architecture
* **KPI Headline Trackers:** Real-time visibility into Total Borrowers, Portfolio Default Rate, High-Risk Capital Exposure, and Average Credit Scores for defaulted accounts.
* **Imbalance Correction Panel:** 100% Stacked Bar Charts analyzing default distribution across `HomeOwnership` and `EmploymentLength` segments.
* **AI-Driven Deep Insights:** Integrated **Decomposition Tree** and **Key Influencers** visuals to map demographic default root causes dynamically.
* **Smart Narratives:** A hybrid automated text summary utilizing embedded dynamic DAX variables for real-time reporting accuracy.

## Tech Stack & Skills Demonstrated
* **BI Platform:** Power BI Desktop
* **Data Modeling:** Advanced DAX (Data Analysis Expressions) for complex financial measures.
* **UI/UX Design:** Clean corporate dashboard architecture with custom responsive tile-slicers for seamless executive navigation.

## Key Insights Discovered
1. **Housing Vulnerability:** Borrowers who currently rent show a significantly higher rate of default compared to homeowners.
2. **Employment Thresholds:** Early-career individuals (less than 1 year of employment length) represent a disproportionate slice of the high-risk segment.

```DAX Formula
1.Avg Credit Score Defaulted = 
CALCULATE(
    AVERAGE('Borrower Dataset'[CreditScore]),
    'Borrower Dataset'[IsDefault] = "Yes"
)

2.Default Rate by Segment = 
DIVIDE(
    CALCULATE(
        COUNTROWS('Borrower Dataset'),
        'Borrower Dataset'[IsDefault] = "Yes"
    ),
    CALCULATE(
        COUNTROWS('Borrower Dataset')
    ),
    0
)

3.High-Risk Capital Exposure = 
CALCULATE(
    SUM('Borrower Dataset'[LoanAmount]),
    'Borrower Dataset'[CreditScore] < 620,
    'Borrower Dataset'[CreditUtilizationRate] >= 0.75,
    'Borrower Dataset'[LoanToIncomeRatio] >= 0.45
)

4.Portfolio Default Rate = 
DIVIDE(
    COUNTROWS(
        FILTER(
            'Borrower Dataset',
            'Borrower Dataset'[IsDefault] = "Yes"
        )
    ),
    COUNTROWS('Borrower Dataset'),
    0
)

5.Triple-Threat Default Rate = 
DIVIDE(
    CALCULATE(
        COUNTROWS('Borrower Dataset'),
        'Borrower Dataset'[IsDefault] = "Yes",
        'Borrower Dataset'[CreditScore] < 620,
        'Borrower Dataset'[CreditUtilizationRate] >= 0.75,
        'Borrower Dataset'[LoanToIncomeRatio] >= 0.45
    ),
    CALCULATE(
        COUNTROWS('Borrower Dataset'),
        'Borrower Dataset'[CreditScore] < 620,
        'Borrower Dataset'[CreditUtilizationRate] >= 0.75,
        'Borrower Dataset'[LoanToIncomeRatio] >= 0.45
    ),
    0
)







