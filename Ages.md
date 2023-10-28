# Age Variables

Age at Report Start

```
=Floor(DaysBetween([Client Date of Birth];[Prompt Report Start])/365.25)
```

Age at Entry

```
=Floor(DaysBetween([Client Date of Birth];[Entry Exit Entry Date])/365.25)
```

Age at Exit/Adjusted End (Current Date if in future)

```

```

Age Buckets - You can also create groups directly in Business Objects by clicking the dots beside of a variable and selecting 'Groups'

```
=If([Client Age at Entry] Between(0;4);"0 - 4";
If([Client Age at Entry] Between(5;12);"05 - 12";
If([Client Age at Entry] Between(13;17);"13 - 17";
If([Client Age at Entry] Between(18;24);"18 - 24";
If([Client Age at Entry] Between(25;34);"25 - 34";
If([Client Age at Entry] Between(35;44);"35 - 44";
If([Client Age at Entry] Between(45;54);"45 - 54";
If([Client Age at Entry] Between(55;61);"55 - 61";
If([Client Age at Entry] Between(62;100);"62 +";
If([Client Age at Entry] <0 Or [Client Age at Entry] >100;"Age Error";[Client Date of Birth Type]))))))))))
```
