### Time drown down 30 Minutes Interval

```
=ArrayFormula(TEXT(ROW(A1:A48)/48,"hh:mm AM/PM"))
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
