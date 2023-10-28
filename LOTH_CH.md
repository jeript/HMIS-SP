# LOTH and CH Variables

CH (X is a Chronic Yes response)

```
=If([Disabling Condition?(1135)]="Yes (HUD)" And [1 Year or More]="X";"X")
```

CH HH (X Means a member of the household is Chronic)

```
=If(Count([Client Uid]) Where([CH]="CH") In([Entry Exit Group UID])>=1;"X")
```

1 Year or More (X means there is more than 1 year of days homeless. Looks at a calculated number of days or Number of months = 12 and number of times either 1 or 4)

```
=If([Days Homeless]>=365;"X";
If([Number of Months]="12" And ([Number Times]="1" Or [Number Times]="4");"X")
)
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
