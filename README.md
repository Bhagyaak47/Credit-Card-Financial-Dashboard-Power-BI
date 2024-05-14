# Credit-Card-Financial-Dashboard-Power-BI


# Objective :
To develop a comprehensive credit card weekly dashboard that provides real-time insights into key performance metrics and trends,
enabling stakeholders to monitor and analyze credit card operations effectively.


# Data Cleaning/ Preparation:
- There are two tables Credit_card.csv(18 Columns & 10108 Rows) & customer.csv.(15 Columns & 10108 Rows)
- Data imported from Mysql Database.
- In customer table created 2 columns i.e, AgeGroup & IncomeGroup.
- In Credit_card table created Revenue Column & week_num 2 column to align week.

# DAX Formulas:
- AgeGroup = SWITCH(
    TRUE(),
    customer[Customer_Age] < 30,"20-30",
    customer[Customer_Age] >=30 && customer[Customer_Age] <40,"30-40",
    customer[Customer_Age] >=40 && customer[Customer_Age] <50,"40-50",
    customer[Customer_Age] >=50 && customer[Customer_Age] <60,"50-60",
    customer[Customer_Age] >=60 ,"60+",
    "unknown")
  - IncomeGroup = SWITCH(
    TRUE(),
    customer[Income] < 35000,"Low",
    customer[Income] >=35000 && customer[Income] < 70000,"Med",
    customer[Income] >=70000 ,"High",
    "unknown")
  - Revenue = credit_card[Annual_Fees]+ credit_card[Total_Trans_Amt]+ credit_card[Interest_Earned]
  - weeknum2 = WEEKNUM(credit_card[Week_Start_Date])
  - Current_week_Revenue = CALCULATE(
    SUM(credit_card[Revenue]),
    FILTER(
        ALL(credit_card),
        credit_card[weeknum2]=MAX(credit_card[weeknum2])))
  - Previous_week_Revenue = CALCULATE(
    SUM(credit_card[Revenue]),
    FILTER(
        ALL(credit_card),
        credit_card[weeknum2]=MAX(credit_card[weeknum2])-1))
  - wow_revenue = DIVIDE(([Current_week_Revenue]-[Previous_week_Revenue]),[Previous_week_Revenue])
 
  ![Credit Card_001](https://github.com/Bhagyaak47/Credit-Card-Financial-Dashboard-Power-BI/assets/152842490/fc009da3-2bb3-4352-8bd4-dc512a3ed938)
  ![Credit Card_002](https://github.com/Bhagyaak47/Credit-Card-Financial-Dashboard-Power-BI/assets/152842490/9fffbdea-e87c-4765-8f67-ba6c8e9caa90)

  # Insights :
  - Overall Revenue is 55M.
  - Total Intrest is 7.8M.
  - Total Transaction Amount is 45M.
  - Male customers are contributing more in Revenue 30M,Female Revenue 25M.
  - Blue & Silver credit card are contributing 46M & 6M revenue.
  - TX,NY & CA is contributing to 68%.
  


