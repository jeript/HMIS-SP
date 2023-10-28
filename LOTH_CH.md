# LOTH and CH Variables

CH (X is a Chronic Yes response)

```
=If([Disabling Condition?(1135)]="Yes (HUD)" And [1 Year or More]="X";"X")
```

1 Year or More (X means there is more than 1 year of days homeless. Looks at a calculated number of days or Number of months = 12 and number of times either 1 or 4)

```
=If([Days Homeless]>=365;"X";
If([Number of Months]="12" And ([Number Times]="1" Or [Number Times]="4");"X")
)
```

Days Homeless (Calculates number of days homeless in current episode)

```
=DaysBetween([Homeless Start Adjusted];[Homeless End Adjusted])
```

Homeless Start Adjusted (Either approx date or Entry date if approx is blank)

```
=If(IsNull([Approximate date this episode of homelessness started(4355)]);[Entry Exit Entry Date];[Approximate date this episode of homelessness started(4355)]
)
```

Homeless End Adjusted (If PH and Housing Move-In Date is on or after Entry then it is move-in date, else if there is an exit then it is exit date, if exit is null then it uses either the current date or the report end date. - I schedule some reports with an End date for the report in the future and then get the last year of data)

```
=If(Match([Entry Exit Provider Program Type Code];"PH*") AND [Housing Move-in Date(5093)]>=RelativeDate([Entry Exit Entry Date];-1);[Housing Move-in Date(5093)];
If(Not(IsNull([Entry Exit Exit Date]));[Entry Exit Exit Date];
If(CurrentDate()>[Report End Date];[Report End Date];CurrentDate()
)))
```

Number Months (Changes text responses for 1 and more than 12 to numeric to match 2-12. More than 12 changes to 12 just because more than 12 doesn't really help any of my calculations)

```
=If(Match([Total number of months homeless on the street, in ES or SH in the past three years(4357)];"One month (this time is the first month) (HUD)");"1";
If(Match([Total number of months homeless on the street, in ES or SH in the past three years(4357)];"More than 12 months (HUD)");"12";
[Total number of months homeless on the street, in ES or SH in the past three years(4357)]
))
```

Number Times - Changes text response to numbers

```
=If(Match([Regardless of where they stayed last night - Number of times the client has been on the streets, in ES, or SH in the past three years including today(4356)];"One time (HUD)");"1";
If(Match([Regardless of where they stayed last night - Number of times the client has been on the streets, in ES, or SH in the past three years including today(4356)];"Two times (HUD)");"2";
If(Match([Regardless of where they stayed last night - Number of times the client has been on the streets, in ES, or SH in the past three years including today(4356)];"Three times (HUD)");"3";
If(Match([Regardless of where they stayed last night - Number of times the client has been on the streets, in ES, or SH in the past three years including today(4356)];"Four or more times (HUD)");"4";
[Regardless of where they stayed last night - Number of times the client has been on the streets, in ES, or SH in the past three years including today(4356)]
))))
```

OLD FORMULAS - NEED TO BE UPDATED

Notes: Requires Entry Objects and Exit Objects Housing Move-In Date

[Homeless Start Adjusted] = If(IsNull([Approximate date homelessness started:(4355)]);[Entry Exit Entry Date];[Approximate date homelessness started:(4355)])

[Move-In Date] = If(Left([Entry Exit Provider Program Type Code];4)="PH -";If([Entry Objects].[Housing Move-in Date(5093)]>RelativeDate([Entry Exit Entry Date];-1);[Entry Objects].[Housing Move-in Date(5093)];If([Exit Objects].[Housing Move-in Date(5093)]>RelativeDate([Entry Exit Entry Date];-1);[Exit Objects].[Housing Move-in Date(5093)])))

[Move-In Date HH] = NoFilter(Min([Move-In Date]) In([Entry Exit Group UID]))

[Days to Move In] = DaysBetween([Entry Exit Entry Date];If([Move-In Date]>[Move-In Date HH];[Move-In Date];[Move-In Date HH]))

[Homeless End Adjusted] =
If(Not(IsNull([Move-In Date]));[Move-In Date];
If(Not(IsNull([Move-In Date HH]));[Move-In Date HH];
If(Not(IsNull([Entry Exit Exit Date]));[Entry Exit Exit Date];
If(CurrentDate()>[Report End Date];[Report End Date];CurrentDate()
))))

[Days Homeless] = DaysBetween([Homeless Start Adjusted];[Homeless End Adjusted])

[CH] =
If([Disabling Condition?(1135)]="Yes (HUD)" And
([Days Homeless]>=365 or
([Total number of months homeless on the street, in ES or SH in the past three years(4357)] InList("More than 12 months (HUD)";"12") AND [Regardless of where they stayed last night - Number of times the client has been on the streets, in ES, or SH in the past three years including today(4356)]="One time (HUD)"));"CH")

[CH HH] = If(Count([Client Uid]) Where([CH]="CH") In([Entry Exit Group UID])>=1;"CH HH")
