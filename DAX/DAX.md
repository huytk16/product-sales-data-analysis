## Core KPI 

* Total Revenue
* Total Profit
* Profit Margin
* Units Sold

## Time Intelligence Measures

* Previous Revenue = CALCULATE([Total Revenue], DATEADD('Date Table'[Date], -1, MONTH))
* *Similar to Previous Profit, Previous Profit Margin and Previous Units Sold*

* MoM Revenue =

var lastest = [Total Revenue]

var previous = [Previous Revenue]

var per =     

    if(
        not ISBLANK(previous) && previous <> 0,
        DIVIDE(lastest - previous, previous), 0
    )

var symbol = 

    switch(
        true(),
        lastest-previous>0, UNICHAR(9650),
        lastest-previous<0, UNICHAR(9660),
        ""
    )
    
return

symbol & " " & format(per, "#0.00%")

* *Similar to MoM Profit, MoM Profit Margin, MoM Units Sold*

## Tooltip

### Clustered column chart

Revenue % by Country = 

DIVIDE(

    [Total Revenue],
    CALCULATE([Total Revenue], ALL('financials'[Country]))
)

### Clustered bar chart

Revenue % by Segment = 

DIVIDE(

    [Total Revenue],
    CALCULATE([Total Revenue], ALL('financials'[Segment]))
)

* *Similar to profit, units sold*
