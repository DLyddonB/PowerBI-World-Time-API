# PowerBI-World-Time-API
This code [taken from here https://oscarvalerock.medium.com/time-of-the-last-refresh-86b87cbd8d91] allows Power BI Desktop and Power BI service to report the same Last Refresh time. 

The problem I had that this code: 

let
    Source = DateTime.LocalNow(),
    #"Converted to Table" = #table(1, {{Source}}),
    #"Changed Type" = Table.TransformColumnTypes(#"Converted to Table",{{"Column1", type datetime}}),
    #"Renamed Columns" = Table.RenameColumns(#"Changed Type",{{"Column1", "Last Refresh Date"}})
in
    #"Renamed Columns"

Returned the time that was displayed on my desktop, but when I published it to Power BI Service it was an hour out (because of the change to BST). 
Anyway, the code in that article seemed to have done the trick nicely! 

