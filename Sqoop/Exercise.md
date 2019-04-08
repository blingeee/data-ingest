# 1. From	the	accounts	table,	import	only	the	primary	key,	along	with	the	first	name,	last	name	to	HDFS	directory /loudacre/accounts/user_info.		Please	save	the	file	in	text	format	with	tab	delimiters.

```
$ sqoop eval --connect  jdbc:mysql://localhost/loudacre --username training --password training --query "describe loudacre.accounts"
19/04/07 23:22:07 INFO sqoop.Sqoop: Running Sqoop version: 1.4.6-cdh5.7.0
19/04/07 23:22:07 WARN tool.BaseSqoopTool: Setting your password on the command-line is insecure. Consider using -P instead.
19/04/07 23:22:07 INFO manager.MySQLManager: Preparing to use a MySQL streaming resultset.
---------------------------------------------------------------------------------------------------------
| Field                | Type                 | Null | Key | Default              | Extra                | 
---------------------------------------------------------------------------------------------------------
| acct_num             | int(11)              | NO  | PRI | (null)               |                      | 
| acct_create_dt       | datetime             | NO  |     | (null)               |                      | 
| acct_close_dt        | datetime             | YES |     | (null)               |                      | 
| first_name           | varchar(255)         | NO  |     | (null)               |                      | 
| last_name            | varchar(255)         | NO  |     | (null)               |                      | 
| address              | varchar(255)         | NO  |     | (null)               |                      | 
| city                 | varchar(255)         | NO  |     | (null)               |                      | 
| state                | varchar(255)         | NO  |     | (null)               |                      | 
| zipcode              | varchar(255)         | NO  |     | (null)               |                      | 
| phone_number         | varchar(255)         | NO  |     | (null)               |                      | 
| created              | datetime             | NO  |     | (null)               |                      | 
| modified             | datetime             | NO  |     | (null)               |                      | 
---------------------------------------------------------------------------------------------------------
```

```
 $ sqoop import --table accounts --connect  jdbc:mysql://localhost/loudacre --username training --password training --columns "acct_num, first_name, last_name" --target-dir /loudacre/accounts/user_info --fields-terminated-by "\t"
```

# 2. This	time	save	the	same	in	parquet	format	with	snappy	compression.		Save	it	in	/loudacre/accounts/user_compressed.		Provide.a	screenshot	of	HUE	with	the	new	directory created.

```
$ sqoop import --table accounts --connect  jdbc:mysql://localhost/loudacre --username training --password training --columns "acct_num, first_name, last_name" --target-dir /loudacre/accounts/user_compressed --fields-terminated-by "\t" --compression-codec org.apache.hadoop.io.compress.SnappyCodec --as-parquetfile
```

# 3. Finally	save	in	/loudacre/accounts/CA	only	clients	whose	state	is	from	California.		Save	the	file in	avro format	and	compressed	using	snappy.		From	the	terminal,	display	some	of	the	records	that	you	just	imported.		Take	a	screenshot	and	save	it	as	CA_only.

```
$ sqoop import --table accounts --connect  jdbc:mysql://localhost/loudacre --username training --password training --where "state='CA'" --target-dir /loudacre/accounts/CA  --compression-codec org.apache.hadoop.io.compress.SnappyCodec --as-avrodatafile
```

명령어 실행후 끝에서 몇개의 데이터만 스크랩 하였습니다.
```
$ avro-tools tojson hdfs://localhost/loudacre/accounts/CA/part-m-00000.avro

{"acct_num":{"int":10167},"acct_create_dt":{"long":1269717428000},"acct_close_dt":{"long":1298652743000},"first_name":{"string":"Marya"},"last_name":{"string":"Wolf"},"address":{"string":"3048 Grove Avenue"},"city":{"string":"San Diego"},"state":{"string":"CA"},"zipcode":{"string":"92017"},"phone_number":{"string":"6198966633"},"created":{"long":1395174606000},"modified":{"long":1395174606000}}
{"acct_num":{"int":10168},"acct_create_dt":{"long":1268455917000},"acct_close_dt":null,"first_name":{"string":"Cathy"},"last_name":{"string":"McCord"},"address":{"string":"2212 Koontz Lane"},"city":{"string":"Oxnard"},"state":{"string":"CA"},"zipcode":{"string":"93025"},"phone_number":{"string":"8050413912"},"created":{"long":1395174606000},"modified":{"long":1395174606000}}
{"acct_num":{"int":10169},"acct_create_dt":{"long":1293121828000},"acct_close_dt":null,"first_name":{"string":"Kory"},"last_name":{"string":"Marshall"},"address":{"string":"1375 Spruce Drive"},"city":{"string":"Industry"},"state":{"string":"CA"},"zipcode":{"string":"91751"},"phone_number":{"string":"6269469513"},"created":{"long":1395174606000},"modified":{"long":1395174606000}}
{"acct_num":{"int":10171},"acct_create_dt":{"long":1271758742000},"acct_close_dt":null,"first_name":{"string":"Shannon"},"last_name":{"string":"Rhymer"},"address":{"string":"994 Comfort Court"},"city":{"string":"North Hollywood"},"state":{"string":"CA"},"zipcode":{"string":"91654"},"phone_number":{"string":"8182168070"},"created":{"long":1395174606000},"modified":{"long":1395174606000}}
{"acct_num":{"int":10172},"acct_create_dt":{"long":1274926065000},"acct_close_dt":null,"first_name":{"string":"Marlyn"},"last_name":{"string":"Beals"},"address":{"string":"3330 Rardin Drive"},"city":{"string":"Sacramento"},"state":{"string":"CA"},"zipcode":{"string":"95854"},"phone_number":{"string":"9160359179"},"created":{"long":1395174606000},"modified":{"long":1395174606000}}
{"acct_num":{"int":10173},"acct_create_dt":{"long":1278251543000},"acct_close_dt":{"long":1350265129000},"first_name":{"string":"Earl"},"last_name":{"string":"Spencer"},"address":{"string":"4002 Byrd Lane"},"city":{"string":"Fresno"},"state":{"string":"CA"},"zipcode":{"string":"93773"},"phone_number":{"string":"5592794420"},"created":{"long":1395174606000},"modified":{"long":1395174606000}}
{"acct_num":{"int":10174},"acct_create_dt":{"long":1286929367000},"acct_close_dt":null,"first_name":{"string":"Charles"},"last_name":{"string":"Lowery"},"address":{"string":"3973 Long Street"},"city":{"string":"Glendale"},"state":{"string":"CA"},"zipcode":{"string":"91257"},"phone_number":{"string":"7470816268"},"created":{"long":1395174606000},"modified":{"long":1395174606000}}
{"acct_num":{"int":10175},"acct_create_dt":{"long":1276918910000},"acct_close_dt":null,"first_name":{"string":"Zane"},"last_name":{"string":"Guerro"},"address":{"string":"2119 Green Acres Road"},"city":{"string":"San Diego"},"state":{"string":"CA"},"zipcode":{"string":"92011"},"phone_number":{"string":"6193564190"},"created":{"long":1395174606000},"modified":{"long":1395174606000}}
{"acct_num":{"int":10176},"acct_create_dt":{"long":1265314179000},"acct_close_dt":{"long":1394059197000},"first_name":{"string":"Jerry"},"last_name":{"string":"Villacorta"},"address":{"string":"3103 Pooz Street"},"city":{"string":"Mojave"},"state":{"string":"CA"},"zipcode":{"string":"93540"},"phone_number":{"string":"6612065308"},"created":{"long":1395174606000},"modified":{"long":1395174606000}}
{"acct_num":{"int":10177},"acct_create_dt":{"long":1263663150000},"acct_close_dt":{"long":1389594186000},"first_name":{"string":"Carolyn"},"last_name":{"string":"Toney"},"address":{"string":"337 Austin Secret Lane"},"city":{"string":"Santa Rosa"},"state":{"string":"CA"},"zipcode":{"string":"95461"},"phone_number":{"string":"7077930811"},"created":{"long":1395174606000},"modified":{"long":1395174606000}}
{"acct_num":{"int":10178},"acct_create_dt":{"long":1280892813000},"acct_close_dt":{"long":1362073634000},"first_name":{"string":"Nancy"},"last_name":{"string":"Walton"},"address":{"string":"2880 Raccoon Run"},"city":{"string":"San Jose"},"state":{"string":"CA"},"zipcode":{"string":"95013"},"phone_number":{"string":"4083188606"},"created":{"long":1395174606000},"modified":{"long":1395174606000}}
{"acct_num":{"int":10179},"acct_create_dt":{"long":1280026842000},"acct_close_dt":null,"first_name":{"string":"Richard"},"last_name":{"string":"Robbins"},"address":{"string":"2744 Sigley Road"},"city":{"string":"Sacramento"},"state":{"string":"CA"},"zipcode":{"string":"94207"},"phone_number":{"string":"9167681842"},"created":{"long":1395174606000},"modified":{"long":1395174606000}}
{"acct_num":{"int":10180},"acct_create_dt":{"long":1288950853000},"acct_close_dt":{"long":1371647862000},"first_name":{"string":"Angel"},"last_name":{"string":"Brown"},"address":{"string":"2583 Arlington Avenue"},"city":{"string":"Pasadena"},"state":{"string":"CA"},"zipcode":{"string":"91136"},"phone_number":{"string":"6261610648"},"created":{"long":1395174606000},"modified":{"long":1395174606000}}
{"acct_num":{"int":10181},"acct_create_dt":{"long":1283095966000},"acct_close_dt":null,"first_name":{"string":"Karen"},"last_name":{"string":"Reed"},"address":{"string":"1236 Hickory Heights Drive"},"city":{"string":"Stockton"},"state":{"string":"CA"},"zipcode":{"string":"95307"},"phone_number":{"string":"2093016544"},"created":{"long":1395174606000},"modified":{"long":1395174606000}}
{"acct_num":{"int":10184},"acct_create_dt":{"long":1264807651000},"acct_close_dt":null,"first_name":{"string":"Michael"},"last_name":{"string":"Whitaker"},"address":{"string":"4631 Green Avenue"},"city":{"string":"Santa Barbara"},"state":{"string":"CA"},"zipcode":{"string":"93185"},"phone_number":{"string":"8055608169"},"created":{"long":1395174606000},"modified":{"long":1395174606000}}
{"acct_num":{"int":10185},"acct_create_dt":{"long":1290664340000},"acct_close_dt":null,"first_name":{"string":"Dave"},"last_name":{"string":"Barber"},"address":{"string":"3529 Don Jackson Lane"},"city":{"string":"Redding"},"state":{"string":"CA"},"zipcode":{"string":"96007"},"phone_number":{"string":"5304039334"},"created":{"long":1395174606000},"modified":{"long":1395174606000}}
{"acct_num":{"int":10188},"acct_create_dt":{"long":1269587441000},"acct_close_dt":null,"first_name":{"string":"Leo"},"last_name":{"string":"Roberts"},"address":{"string":"3253 Blane Street"},"city":{"string":"San Francisco"},"state":{"string":"CA"},"zipcode":{"string":"94039"},"phone_number":{"string":"4152074452"},"created":{"long":1395174606000},"modified":{"long":1395174606000}}
{"acct_num":{"int":10189},"acct_create_dt":{"long":1269177174000},"acct_close_dt":null,"first_name":{"string":"Ken"},"last_name":{"string":"Lee"},"address":{"string":"1501 Juniper Drive"},"city":{"string":"Eureka"},"state":{"string":"CA"},"zipcode":{"string":"95589"},"phone_number":{"string":"7078812040"},"created":{"long":1395174606000},"modified":{"long":1395174606000}}

```