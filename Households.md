# Household Related Variables

Relationship to Head of Household Error (0 or Multiple HoH return an X which can be useful for formatting rules)

```
=NoFilter(If(Count([Client Uid]) Where([Relationship to Head of Household(3375)]="Self (head of household)") In([Entry Exit Group UID])<>1;"X"))

```

Household Type - The NoFilter() allows filtering a report for only HoH and still identify the type

```
=(If(NoFilter(Count([Client Uid])) In([Entry Exit Group UID])=1 And ([Client Age at Entry]>=18 Or IsNull([Client Age at Entry]));"SA";
If(NoFilter(Count([Client Uid])) In([Entry Exit Group UID])=1 And [Client Age at Entry]<18;"UM";
If(NoFilter(Count([Client Uid])) In([Entry Exit Group UID])>1 And NoFilter(Count([Client Uid])) In([Entry Exit Group UID]) = NoFilter(Count([Client Uid]) Where([Client Age at Entry]>=18)) In([Entry Exit Group UID]);"AO";
"AC"
))))
```

Number of Household Members

```
=NoFilter(Count([Client Uid])) In([Entry Exit Group UID])
```
