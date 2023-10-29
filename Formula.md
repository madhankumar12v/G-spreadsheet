### Time drown down 30 Minutes Interval

```
=ArrayFormula(TEXT(ROW(A1:A48)/48,"hh:mm AM/PM"))
```
### Split Text or Number with Delimiter

```
=RIGHT(A1, LEN(A1) - FIND("-", A1))

=LEFT(A1, FIND("-", A1) - 1)

```


### CONCATENATE Formula with Line break

```
=CONCATENATE("*Booking confirmation from thrillophilia*"&CHAR(10),
"Internal ID: "&B3&CHAR(10),
"PNR: "&A3&CHAR(10),
"Nights/Days: "&F3&CHAR(10),
"Booking type: "&I3&CHAR(10),
"Journey date: "&TEXT(G3,"mmmm-dd")&CHAR(10),
"Locations covered: "&J3&CHAR(10),
"Food Plan: "&K3&CHAR(10),
"Passenger count: " &N3&"-Adults + "&O3&"-childrens"&"("&Q3&") + "&P3& "-infant"&CHAR(10),
"Car type: "&S3&CHAR(10),
"pickup/drop location: "&AC3&" / "&AD3&CHAR(10),
"Cab days: "&AA3&CHAR(10),
"Vendor budget: "&V3&CHAR(10),
"*--------*"&CHAR(10),

IF(ISBLANK(AI3),"","*Hotel preference*"&CHAR(10)),
IF(ISBLANK(AI3),"",AI3&CHAR(10)),

IF(ISBLANK(AJ3),"",AJ3&CHAR(10)),
IF(ISBLANK(AK3),"",AK3&CHAR(10)),
IF(ISBLANK(AL3),"",AI3&CHAR(10)),
IF(ISBLANK(AM3),"",AM3&CHAR(10)),
IF(ISBLANK(AN3),"",AN3&CHAR(10)),
"*--------*"&CHAR(10),

IF(ISBLANK(AI4),"","*Hotel Night order*"&CHAR(10)),
IF(ISBLANK(AI4),"","1st night: "&AO4&CHAR(10)),
IF(ISBLANK(AP4),"","2nd night: "&AP4&CHAR(10)),
IF(ISBLANK(AQ4),"","3rd night: "&AQ4&CHAR(10)),
IF(ISBLANK(AR4),"","4th night: "&AR4&CHAR(10)),
IF(ISBLANK(AS4),"","5th night: "&AS4&CHAR(10)),
IF(ISBLANK(AT4),"","6th night: "&AT4&CHAR(10)),
IF(ISBLANK(AU4),"","7th night: "&AU4&CHAR(10)),



)

```

### Count_IF Formula

```
COUNT(IF(Booking intimaion="FALSE" and t0._n31482148_!=TODAY(),1,Null))+COUNT(IF(Hotel confirmation message to customer="FALSE" and t0._n31482148_!=TODAY(),1,Null))+COUNT(IF(Rev ed start="FALSE" and t0._n31482148_!=TODAY(),1,Null))+COUNT(IF(Rev ed end="FALSE" and t0._n31482148_!=TODAY(),1,Null))+COUNT(IF(Chat & inv check="Issue" and t0._n31482148_!=TODAY(),1,Null))+COUNT(IF(Chat & inv check="." and t0._n31482148_!=TODAY(),1,Null))+
COUNT(IF(Vehicle status="alloted" and t0._n31482148_!=TODAY(),1,Null))+COUNT(IF(Vehicle status="Yet to" and t0._n31482148_!=TODAY(),1,Null))+COUNT(IF(Vehicle status="." and t0._n31482148_!=TODAY(),1,Null))+
COUNT(IF(Hotel status="Yet" and t0._n31482148_!=TODAY(),1,Null))+COUNT(IF(Hotel status="Requested" and t0._n31482148_!=TODAY(),1,Null))+COUNT(IF(Hotel status="Booked" and t0._n31482148_!=TODAY(),1,Null))+COUNT(IF(Hotel status="NA" and t0._n31482148_!=TODAY(),1,Null))

```

### CASE Formula

```
CASE
  WHEN booking = 'avm' THEN 'Pending'
  WHEN booking = 'madhan' THEN 'Completed'
  ELSE NULL
END

```
### Import Current Month data only

```
=FILTER('G-booking Backend'!A2:A13122, MONTH('G-booking Backend'!B2:B13122) = MONTH(TODAY()))

```

### Import Current specific month data ("Mention the Month")
```
=FILTER('G-booking backend'!A2:A13122, TEXT('G-booking backend'!B2:B13122, "mmmm") = "June")

```


### Automatically Increase Number when text appear B column

```
=IF(B3<>"","TR"&TEXT(ROW(B3)-ROW(B$3)+1,"00"),"")

=IF(B1<>"","TR"&TEXT(ROW(B1)-ROW(B$1)+1,"00"),"")

```
### Google Sheet Query

```
=TRANSPOSE(QUERY('Transport Backend'!$A$2:$I$92,"Select B where A = '"&$N11&"'"))
```

```
=TRANSPOSE(QUERY($D$23:$F$28,"select F where D ='"&$G23&"' and E ='"&$H23&"'"))
```

```
=TRANSPOSE(QUERY($C$23:$F$28,"select F where C ='"&$G23&"' and D ='"&$H23&"' and E = "&$I23&" "))
```

### Import specific month and Year data ("Mention the Month & Year")
```
=QUERY(IMPORTRANGE("https://docs.google.com/spreadsheets/d/1hdBaRUt62UfDc_LYOAEBPiermHCWAfCXbUiQ-1U-HNg/edit#gid=0", "Sheet1!A:I"), "SELECT * WHERE MONTH(Col9) = 6 AND YEAR(Col9) = 2023")
```

### Text to Date Convert Formula
```
=ARRAYFORMULA(IFERROR(IFERROR(REGEXREPLACE(B2:B, 
 "(\d+)/(\d+)/(\d{2,4})", "$2/$1/$3")*1, B2:B)*1, B2:B))
```

### Formula
```
=IFERROR(TRIM(UPPER(SUBSTITUTE($B2,"-","")&VALUE($A2)))," ")
```

### Check if cell is not  blank then concate two cell other wise " "
```
=IF(AND(A2<>"",B2<>""),TRIM(CONCATENATE(A2,B2))," ")
```

### Filter the data with Condition
```
=FILTER(C:C,C:C<>" ")
```

### Remove the duplicates
```
=UNIQUE(A:A)
```

### Remove the Duplicate with Conditon
```
=UNIQUE(FILTER(C2:C, C2:C<>" "))
```

### Import specific sheet
```=IMPORTRANGE("https://docs.google.com/spreadsheets/d/1S_pJ5WTt4vIQskHzfgsj6xhwBWnpyYPts1zk_PBEtuI", "SheetName!A22610:H")
```
