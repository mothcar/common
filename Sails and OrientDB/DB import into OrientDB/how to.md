## Reference
[luigidellaquila](https://github.com/mothcar/wkt-to-orient)  

create DB and set class to geospatial property
```
orientdb> create database <databaseName>
orientdb> create class <className> extends V
orientdb> create property <className>.location embedded OPoint
```
`<className>.location` 에서 `location`은 변수명으로써 사용자가 설정하면 된다. 중요한건 OPoint이다. 이것은 이미 선언된 system class이다.



//
