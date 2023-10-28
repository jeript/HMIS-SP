# Demographic Variables

Suggestions for better ways of reporting these both sensitive and important identities are very welcomed.

Gender

```
=If([Gender(894)]="Man (Boy, if child); Transgender";"Transgender Man";
If([Gender(894)]="Woman (Girl, if child); Transgender";"Transgender Woman";
If([Gender(894)]="Man (Boy, if child); Questioning";"Man, Questioning";
If([Gender(894)]="Woman (Girl, if child); Questioning";"Woman, Questioning";
If(Match([Gender(894)];"_;_");"No Single Gender";
If(IsNull([Gender(894)]); "Missing Value";[Gender(894)]))))))
```

Race and Ethnixcity

```
=If([Race and Ethnicity(7762)]="Hispanic/Latina/e/o; White" Or [Race and Ethnicity(7762)]="Hispanic/Latina/e/o";"Hispanic/Latina/e/o";
If(Match([Race and Ethnicity(7762)];"*Latina*");"Hispanic/Latina/e/o Multiracial";
If(Match([Race and Ethnicity(7762)];"*;*");"Multiracial";[Race and Ethnicity(7762)]
)))
```
