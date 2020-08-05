# Wrap JSON to multi lines / Test ISJSON 
~~~
   This is a coding example working on Caché 2018.1.3 and IRIS 2020.2
   It will not be kept in sync with new versions   
   It is also NOT serviced by InterSystems Support !
~~~

### install and usage ###  
Packed Pretty.xml installs routine ZPretty in any namespace.  
calling $$Do^ZPretty(input,\[filler],\[newline]) returns a wrapped JSON string.   
_filler_ is the optional string for the indent, default = "  "  
_newline_ is optional, default =  $C(13,10)  <CR><LF>    
_input_ accepts: JSON_String, JSON_Stream, %DynamicAbstractObject  

^Pretty leaves all error trapping to you. So can use it as ISJSON check.  

Set flat=$$Do^Pretty(input,"","") removes all formatting from input.  
this could be useful to compare 2 differn formatte JSON_Strings. 

### examples ###  
~~~
USER>read jsn
{"Name":"Li,Robert K.","SSN":"672-92-9664","DOB":"1975-01-12","Home":{"Street":"986 Washington Blvd","City":"Boston","State":"PA","Zip":"95802"},"Office":{"Street":"6012 First Place","City":"Reston","State":"MT","Zip":"77739"},"Spouse":{"Name":"Avery,Zelda H.","SSN":"323-13-7437","DOB":"1943-03-27","Home":{"Street":"196 Main Drive","City":"Youngstown","State":"WY","Zip":"53229"},"Office":{"Street":"4056 Franklin Court","City":"Bensonhurst","State":"IA","Zip":"27688"},"FavoriteColors":["Black"],"Age":77},"Age":45,"Title":"Associate Marketing Manager","Salary":10421}
USER>
~~~~  
##### straight to device #####   
~~~
USER>write $$Do^ZPretty(jsn)
{
  "Name":"Li,Robert K.",
  "SSN":"672-92-9664",
  "DOB":"1975-01-12",
  "Home":{
    "Street":"986 Washington Blvd",
    "City":"Boston",
    "State":"PA",
    "Zip":"95802"
  },
  "Office":{
    "Street":"6012 First Place",
    "City":"Reston",
    "State":"MT",
    "Zip":"77739"
  },
  "Spouse":{
    "Name":"Avery,Zelda H.",
    "SSN":"323-13-7437",
    "DOB":"1943-03-27",
    "Home":{
      "Street":"196 Main Drive",
      "City":"Youngstown",
      "State":"WY",
      "Zip":"53229"
    },
    "Office":{
      "Street":"4056 Franklin Court",
      "City":"Bensonhurst",
      "State":"IA",
      "Zip":"27688"
    },
    "FavoriteColors":[
      "Black"
    ],
    "Age":77
  },
  "Age":45,
  "Title":"Associate Marketing Manager",
  "Salary":10421
}
USER>
~~~

##### to string & compare #####   
~~~
USER>set wrap=$$Do^ZPretty(jsn)

USER>write $s(wrap=jsn:"SAME",1:"DIFF")
DIFF
USER>write $s($$Do^ZPretty(wrap,"","")=jsn:"SAME",1:"DIFF")
SAME
~~~

##### ISJSON #####   
~~~
USER>set crap=$replace(wrap,"""Home"":","")
USER>do Do^ZPretty(crap)
<THROW>%FromJSON+38^%Library.DynamicAbstractObject.1 *%Exception.General Parsing error 3 Line 5 Offset 3

USER>try {do Do^ZPretty(jsn) Write "OK" IF 1} catch er { Write "NO" IF 0 } write !,$test
OK
1
USER>try {do Do^ZPretty(crap) Write "OK" IF 1} catch er { Write "NO" IF 0 } write !,$test
NO
0
~~~

[Article in DC](https://community.intersystems.com/post/wrap-json-multi-lines-test-isjson)
