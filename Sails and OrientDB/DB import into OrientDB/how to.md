## Reference
[luigidellaquila](https://github.com/mothcar/wkt-to-orient)  

## Environment
sample CSV file.
Be ready OrientDB Studio using Terminal.
```
$ ./server.sh
```
install npm modules
```
npm install orientjs
npm install fast-csv
```

Then create DB and set class to geospatial property
```
orientdb> create database <databaseName>
orientdb> create class <className> extends V
orientdb> create property <className>.location embedded OPoint
```
`<className>.location` 에서 `location`은 변수명으로써 사용자가 설정하면 된다. 중요한건 OPoint이다. 이것은 이미 선언된 system class이다.

javascript using localhost id and password  
insert properties : 3 (name, location, type)  
CSV data : data.full_name, data.type, 
위에서 location은 빠져있는데 이유는 파싱이 좀 복잡하다. *ST_GeomFromText*를 사용하는데 이 문법은 [이곳](http://www.postgis.org/docs/ST_GeomFromText.html)을 참조한다.  
```
var insertElement = function(data){
  queue++;
	console.log("data.WKT :: ", data.WKT)
	db.insert().into(className).set({
		name: data.full_name,
		location: db.rawExpression("ST_GeomFromText("+"'POINT " +"("  +data.longitude+ " " +data.latitude+ ")" +"')"),
		type: data.type
	})
	.one().then(function(){
		  i++;
      queue--;
	    checkFinished();
    }).catch(function(error){
	    queue--;
    	checkFinished();
    	console.log(error)
    });
}
```

Execute
```
$ node csvimport.js POI data/poland-poi.csv 
```
>> node`node명령어` csvimport.js`실행파일` POI`className` data/poland-poi.csv`CSV파일`   




//
