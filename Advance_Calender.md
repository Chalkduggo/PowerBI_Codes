Calender = 
VAR MinDate = MIN('Table'[Date])
Var MaxDate = Max('Table'[Date])
var _startOfFiscalYear=1
VAR Days = CALENDAR ( MinDate, MaxDate )
return
ADDCOLUMNS(
    Days,
"Year",YEAR([Date]),
"Start of Year",DATE( YEAR([Date]),1,1),
"End of Year",DATE( YEAR([Date]),12,31),
"Month",MONTH([Date]),
"Start of Month",DATE( YEAR([Date]), MONTH([Date]), 1),
"End of Month",EOMONTH([Date],0),
"Days in Month",DATEDIFF(DATE( YEAR([Date]), MONTH([Date]), 1),EOMONTH([Date],0),DAY)+1,
"Year Month Number",INT(FORMAT([Date],"YYYYMM")),
"Year Month Name",FORMAT([Date],"YYYY-MMM"),
"Day",DAY([Date]),
"Day Name",FORMAT([Date],"DDDD"),
"Day Name Short",FORMAT([Date],"DDD"),
"Day of Week",WEEKDAY([Date]),
"Day of Year",DATEDIFF(DATE( YEAR([Date]), 1, 1),[Date],DAY)+1,
"Month Name",FORMAT([Date],"MMMM"),
"Month Name Short",FORMAT([Date],"MMM"),
"Quarter",QUARTER([Date]),
"Quarter Name","Q"&FORMAT([Date],"Q"),
"Year Quarter Number",INT(FORMAT([Date],"YYYYQ")),
"Year Quarter Name",FORMAT([Date],"YYYY")&" Q"&FORMAT([Date],"Q"),
"Start of Quarter",DATE( YEAR([Date]), (QUARTER([Date])*3)-2, 1),
"End of Quarter",EOMONTH(DATE( YEAR([Date]), QUARTER([Date])*3, 1),0),
"Week of Year",WEEKNUM([Date]),
"Start of Week", [Date]-WEEKDAY([Date])+1,
"End of Week",[Date]+7-WEEKDAY([Date]),
"Fiscal Year",if(_startOfFiscalYear=1,YEAR([Date]),YEAR([Date])+ QUOTIENT(MONTH([Date])+ (13-_startOfFiscalYear),13)),
"Fiscal Quarter",QUARTER( DATE( YEAR([Date]),MOD( MONTH([Date])+ (13-_startOfFiscalYear) -1 ,12) +1,1) ),
"Fiscal Month",MOD( MONTH([Date])+ (13-_startOfFiscalYear) -1 ,12) +1,
"Day Offset",DATEDIFF(MaxDate,[Date],DAY),
"Month Offset",DATEDIFF(MaxDate,[Date],MONTH),
"Quarter Offset",DATEDIFF(MaxDate,[Date],QUARTER),
"Year Offset",DATEDIFF(MaxDate,[Date],YEAR)
)
