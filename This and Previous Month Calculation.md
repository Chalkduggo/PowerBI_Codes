//This Month
Selected_Value_This_Month = 
CALCULATE(
    [Selected Calculation],
    YEAR('Combined OTT'[Date]) = YEAR(MAX('Combined OTT'[Date])),
    MONTH('Combined OTT'[Date]) = MONTH(MAX('Combined OTT'[Date]))
)


// previous month
Selected_Value_Previous_Month = 
VAR Current_Month = MONTH(MAX('Combined OTT'[Date]))
VAR Current_Year = YEAR(MAX('Combined OTT'[Date]))    
VAR Previous_Month = IF(Current_Month = 1, 12, Current_Month - 1)
VAR Previous_Year = IF(Current_Month = 1, Current_Year - 1, Current_Year)

RETURN
CALCULATE(
    [Selected Calculation],
    MONTH('Combined OTT'[Date]) = Previous_Month,
    YEAR('Combined OTT'[Date]) = Previous_Year
)
