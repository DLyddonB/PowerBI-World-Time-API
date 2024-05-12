# PowerBI-World-Time-API

So these are the steps to get the LastRefresh time consistent on your Power BI Desktop and on Power BI as a service

1. Go to the PowerQuery window and select 'New Source' and choose web.
2. Paste the following URL: http://worldtimeapi.org/api/timezone (this will show you all available timezones. To be honest this step can be skipped and go straight to 3.)
3. Paste the following URL: http://worldtimeapi.org/api/timezone/Europe/London
4. Next, convert it to a table
5. The go to 'Transform' and click 'Transpose'
6. Then click on the 'Promote first row to headers option'
7. Finally, find the column called 'datetime' and change the Type to Date/Time/Timezone.
8. Done!

Now in theory, when you drag and drop this onto a card it will return the current time. 

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

