# Day Calculations

Most formulas use dates from [Dates.md](./Dates.md)

Total Days Enrolled (Remove +1 for nights)

```
=DaysBetween([Entry Exit Entry Date];[Adjusted Exit])+1
```

Days to Move In

````
=DaysBetween([Entry Exit Entry Date];If([Move-In Date]>[Move-In Date Household];[Move-In Date];[Move-In Date Household]))```

Days Homeless (Calculates number of days homeless in current episode)

```
=DaysBetween([Homeless Start Adjusted];[Homeless End Adjusted])
```

Will work on adding more soon!
````
