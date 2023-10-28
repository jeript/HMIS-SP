# Date Variables

Report Prompt Start Date - Adjust "Report Start Date:" to your start prompt

```
=If(IsError(ToDate(UserResponse("Report Start Date:");"M/dd/yyyy h:mm:ss a"));ToDate(UserResponse("Report
Start Date:");"M/dd/yyyy");ToDate(UserResponse("Report Start Date:");"M/dd/yyyy h:mm:ss a"))
```

Report Prompt End Date - Adjust "Report End Date (Plus One Day):" to match your end date prompt

```
=RelativeDate(If(IsError(ToDate(UserResponse("Report End Date (Plus One Day):");"M/dd/yyyy h:mm:ss a"));ToDate(UserResponse("Report
 End Date (Plus One Day):");"M/dd/yyyy");ToDate(UserResponse("Report End Date (Plus One Day):");"M/dd/yyyy h:mm:ss a"));-1)
```

Adjusted Exit - Add exit date for stayers for length of stay and other calculations

````
=If(IsNull([Entry Exit Exit Date]) Or [Entry Exit Exit Date]>=[Report End Date];RelativeDate([Report End Date];-1);[Entry Exit Exit Date]
)```
````

Move-In Date - Makes sure project is PH and Move-In is during the enrollment period

```
=If(Match([Entry Exit Provider Program Type Code];"PH*") And [Housing Move-in Date(5093)]>RelativeDate([Entry Exit Entry Date];-1) And [Housing Move-in Date(5093)]<=[Entry Exit Exit Date];[Housing Move-in Date(5093)])
```

Move-In Date Household - Uses previous Move-In Date Formula and populates the HoH date to other members
=If(isNull([Move-In Date]);[Move-In Date] Where([Relationship to Head of Household(3375)]="Self (head of household)") In([Entry Exit Group UID]); [Move-In Date])
