## Purpose

This file documents the intent, structure, and maintenance approach for the Power BI artefact associated with the NHS Wales finance project.

## Main artefact

dashboard/NHS_Wales_Financial_Dashboard.pbix

What this .pbix should contain

The BI build report describes a report designed around three analytical pages:
1.Spending Pressures & Growth Drivers
2.Equity & Per-Head Resource Efficiency
3.Allocation Shifts & Funding Mix


Report tabs

01_Overview
A concise landing page with:
title and project subtitle
project description
latest-year KPIs
short “how to use this report” note


02_Spending_Pressures

Purpose:
identify large categories
identify categories with unusual or sustained growth
examine year-on-year pressure points

visuals:
KPI cards
total expenditure trend
current spend by category
YoY absolute change by category
YoY growth % by category
pressure watchlist table

03_Equity_Per_Head

Purpose:
compare boards fairly after population normalisation
benchmark against Wales
surface persistent variation

visuals:
per-head ranking by board
difference vs Wales benchmark
distribution table
category spread watchlist
optional small multiples by board

04_Allocation_Shifts

Purpose:
reveal how the funding mix changed
highlight gainers and losers in budget share

visuals:
stacked area chart
percentage-point change bars
funding shift table
current share vs change scatter plot


05_Method_Notes

Optional documentation page with:
totals-only rule
COVID period definition
metric definitions
limitations / interpretation guidance


Model structure

FactFinance
DimCategory
DimFinancialYear
DimHealthBoard


Relationship pattern

FactFinance[CategoryBreakdown] → DimCategory[CategoryBreakdown]
FactFinance[FinancialYear] → DimFinancialYear[FinancialYear]
FactFinance[HealthBoard] → DimHealthBoard[HealthBoard]

Metric governance

The rules:
executive pages use totals only
subcategories are for drill-down or diagnostics
per-head metrics are not mixed with absolute expenditure visuals without explicit labels
percentage-of-total is treated as a separate analytical lens


Core DAX areas

Typical measures needed:
Total Expenditure
Total Per Head
Total PctTotal
Previous Year Value
YoY Change
YoY Growth %
Wales PerHead
Difference vs Wales
Difference vs Wales %
Baseline PctTotal
Percentage Point Shift
