# DAX Measures (starter list)

Delivered_PO_Count =
    COUNTROWS( FILTER( 'PO', 'PO'[DeliveredFlag] = TRUE ) )

OnTime_PO_Count =
    COUNTROWS(
        FILTER(
            'PO',
            'PO'[DeliveredFlag] = TRUE
            && 'PO'[DeliveredDate] <= 'PO'[DueDate]
        )
    )

OnTime_Rate =
    DIVIDE( [OnTime_PO_Count], [Delivered_PO_Count] )

OpenPO_Value =
    SUMX(
        FILTER( 'PO', 'PO'[Status] = "Open" ),
        'PO'[RemainingQty] * 'PO'[UnitPrice]
    )

Projected_Balance =
    SUM( 'PO'[ProjectedBalance] )

InStock_Value =
    SUM( 'Inventory'[OnHandQty] * 'Inventory'[UnitCost] )

PO_Age_Days =
    DATEDIFF( 'PO'[DueDate], TODAY(), DAY )

PO_Age_Bucket =
    SWITCH(
        TRUE(),
        [PO_Age_Days] <= 30, "0–30 Days",
        [PO_Age_Days] <= 60, "31–60 Days",
        [PO_Age_Days] <= 90, "61–90 Days",
        "90+ Days"
    )

PO_Completed_By_Month =
    FORMAT( 'PO'[DeliveredDate], "MMMM" )   // for the column used in the column chart
