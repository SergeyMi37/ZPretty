# Wrap JSON to multi lines
~~~
   This is a coding example working on Caché 2018.1.3 and IRIS 2020.2
   It will not be kept in synch with new versions   
   It is also NOT serviced by InterSystems Support !
~~~

### install and usage ###  
Packed Pretty.xml installs class ZPretty in any namespace.  
calling $$Do^ZPretty(input,\[filler],\[newline]) returns wrapped JSON string 
It's up to the you to Write it out or fill ir inot a stream
ZJ.Pretty is a %Registered object and needs an instance to run the methdos.

### examples ###  
~~~
USER>read jsn
{"Name":"Cunningham,John C.","SSN":"294-11-9150","DOB":"1933-01-08","Home":{"Street":"4249 Ash Street","City":"Tampa","State":"MD","Zip":"30176"},"FavoriteColors":["White","Red","Green"]}
USER>
~~~~  
##### straight to device #####   
~~~
USER>do ##class(ZJ.Pretty).%New().Format(jsn)
{
  "Name":"Cunningham,John C.",
  "SSN":"294-11-9150",
  "DOB":"1933-01-08",
  "Home":{
    "Street":"4249 Ash Street",
    "City":"Tampa",
    "State":"MD",
    "Zip":"30176"
  },
  "FavoriteColors":[
    "White",
    "Red",
    "Green"
  ]
}
USER>
~~~

##### to string #####   
~~~
USER>do ##class(ZJ.Pretty).%New().FormatToString(jsn,.out)
USER>write out
{
  "Name":"Cunningham,John C.",
  "SSN":"294-11-9150",
  "DOB":"1933-01-08",
  "Home":{
    "Street":"4249 Ash Street",
    "City":"Tampa",
    "State":"MD",
    "Zip":"30176"
  },
  "FavoriteColors":[
    "White",
    "Red",
    "Green"
  ]
}
USER>
~~~

##### to stream #####   
~~~
USER>do ##class(ZJ.Pretty).%New().FormatToStream(jsn,.stream)
USER>do stream.OutputToDevice()
{
  "Name":"Cunningham,John C.",
  "SSN":"294-11-9150",
  "DOB":"1933-01-08",
  "Home":{
    "Street":"4249 Ash Street",
    "City":"Tampa",
    "State":"MD",
    "Zip":"30176"
  },
  "FavoriteColors":[
    "White",
    "Red",
    "Green"
  ]
}
USER>
~~~
