# UNI-T Scanner

```

The broadcast bits brakedown
HEX: Ox020106080955543338334254030312FF14FFAABB10053A020313533344C55583B30000425

LEN 2 | TYPE 0x01 | VALUE 0x06

8       0x09        0x55543338334254 

3       0x03        0x12FF

20      OxFF        OxAABB10053A20203135
					33364C55583B30000427

This is the RAW data that enviroment sensor broadcasts
```

 

```hex
So if we look at the data:

Ox020106080955543338334254030312FF14FFAABB10053A020313533344C55583B30000425

and that converted to string:

'	UT383BTÿÿª»: 1534LUX;0%'


Like so:

echo Ox020106080955543338334254030312FF14FFAABB10053A020313533344C55583B30000425 | xxd -r -p

	UT383BT����:S3D�U��B%


--- Ugly

```

```
What we acually want is name: UT383BT and value: 1534LUX

Which are as follows:


HEX: 020106080955543338334254030312FF14FFAABB10053A 020313533344C55583B30000425 

TO 

STRING: '	UT383BTÿÿª»: 1534LUX;0%'

So:

HEX: 55543338334254 STRING: 'UT383BT' 
HEX: 313533344C5558 STRING: '1534LUX'
```

```
So we should be able to locate from where to parse HEX data and convert that to string to add to the TSDB.

Problem, the value isn't always the same so need to check if simple logik could handle it. 

example:

echo 5554333833425420313533344C5558 | xxd -r -p
UT383BT 1534LUX%
```


