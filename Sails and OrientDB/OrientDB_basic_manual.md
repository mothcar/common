이 문서는 Sails JS를 환경으로 한 설명이다.
***
테이블 생성 : orientdb에서는 테이블을 class로 한다.
```
create class <someClassName>
```

Geospatial에 특화된 library 설치
cf) http://orientdb.com/docs/2.2/Spatial-Index.html  
위 링크에서 **install** 참조  
Download orientdb-spatial-2.2.22-dist.jar  
```
$ curl -O http://central.maven.org/maven2/com/orientechnologies/orientdb-spatial/2.2.22/orientdb-spatial-2.2.22-dist.jar  
```
move file to **orientdb/lib/orientdb-spatial-2.2.22-dist.jar**  

orientdb를 실행시키고  
POI class를 만들고 property를 넣어보자.
```
> create class POI
> create property POI.location EMBEDDED OPoint
```
이것의 결과로 POI의 schema가 일반적인 것들과 다르게 나온다.
![](https://github.com/mothcar/common/blob/master/images/poi.jpg)  
또한 system classes가 4페이지(전에는 2페이지)로 늘어난것을 확인할 수 있다.  
![](https://github.com/mothcar/common/blob/master/images/poly.jpg)  
select from POI limit 100 // 기본으로 limit이 30정도에 걸려 있어서 DB가 없는 줄 알 수 있다.  
***  
준비중...
