# Class  
## create Class
```sql
> create class <className> extends V
```


# Edge  
## create Edge
```sql
> create class <edgeName> extends E
```
## create Edge Record
```sql
> create edge write from #49:0 to #41:81 set comment = 'nice product'
```
## show Edge Record
```sql
> select *, expand(inE('write')) from post
``` 
### Reference : [LINK](https://stackoverflow.com/questions/28534120/orientdb-sql-query-to-select-edge-and-vertex-fields-property) 

<br/>  

 

# Common  
## select record   

```sql
> select from post order by createdAt desc
```

## delete record
`className`에서 `columnName`인 곳에서 `a`로 시작되는 값들을 지워라.  
특별히 `delete vertex`로 한 것은 이 값들이 단순히  `class`가 아닌`vertex`이기때문에 그렇다.
```sql
> delete vertex from post where content like '%a'
> delete vertex from post where @rid=#41:7
```
a로 시작하는 모든것을 삭제
```sql
> delete vertex from post where content like 'a%'
```
영어로 된 모든 것 삭제
```sql
> delete vertex from post where content BETWEEN 'a' and 'z'
```
영어를 포함한 숫자들 삭제
```sql
> delete vertex from post where content MATCHES '[A-Z0-9._%+-]'
```

## cases

시간을 조건으로 select
```sql
> select from post where createdAt  between '2018-01-21 08:12:42' and '2018-01-21 08:14:42'  
```
위 응용 		
```sql
> update (select from post where createdAt  between '2018-01-21 08:12:42' and '2018-01-21 08:14:42') increment view_level = 10
```
위 응용 where condition	
```sql
> update post increment view_level = -10 where createdAt  between '2018-01-21 08:12:42' and '2018-01-21 08:14:42'
```
Add to array 	
```sql
> update #32:50 add channel = "aaa"
```
Remove from array		
```sql
> update #32:50 remove channel = "aaa"
```
Json 새필드 추가		
```sql
> update #22:2 merge {"@type":"d","@version":0,"char":"philosopy"}
```
Json 필드 update		
```sql
> update #22:2 merge {"humanity":{"@type":"d","@version":0,"char":"philosopy"}}
```
위험함 레코드 전체를 리셋함
```sql
> update #22:2 content {"humanity":{"type":"new"}}
```
필드에 배열 데이터 넣기	
```sql
> update Users set affiliated = [#33:31, #33:32] where @rid=#24:0
```
필드가 array인 경우 element
```sql
> select from users where affiliated contains #33:31
```
Json element 추가		
```sql
> update users put humanity= 'peach', 10 where @rid = #23:1  // “@type”=”d”, “@version=’” 삭제후 
```

이전 방법은 ‘embedded를 사용하지 않았을때이고 이 다음부터는 embedded를 사용해서 입력한 예 먼저 property 설정
Json 필드를 활성화하기위해 EMBEDDEDLIST 입력 	 
```sql
> CREATE PROPERTY Users.humanity EMBEDDEDSET STRING / CREATE PROPERTY Users.about_info EMBEDDEDSET STRING
```
Json 필드에 element없으면 처음에는 입력 	 
```sql
> insert into Users set about_info = [{"@type":"d","@class":"Adress","city":"london", "zipcode":"4323"}] where @rid = #21:6
```
위 절차는 안해도 된다. setting후 최초입력하면 [“”]	 
```sql
> update Users add about_info = [{"@type":"d","@class":"sample","city":"lisbon", "zipcode":"1516"}] where @rid = #21:0
```
Json element 추가 			 

```sql
> update Users add about_info = [{"@type":"d","@class":"Adress","city":"lisbon", "zipcode":"1516"}] where @rid = #21:6
> update Users set humanity= {"@type":"d", "Name":"George", "Age":"32"}
> update Users add humanity= {"@type":"d", "aa":"bb", "cc":"dd"}
> update Users add humanity= {"@type":"d", name:"somename"}
> update Users add about_info= {name:"somename"}

```
추가 sql 		 
```sql
> update Users add about_info="+about_info+", humanity=" +humanity+" where @rid=" + user_id
```
Embedded List 일때 Json 필드내에 element 수정 
```sql
> update users set about_info[5] = {"@type":"d","@version":0,"sports":"soccer"} where @rid= #21:0
```
Embedded SET 일때 	 
```sql
> update users set humanity[0].telephone = '0000' where @rid= #21:0
```
2개이상 수정일때 		 
```sql
> update users set humanity[0].telephone = '010-7168-1777', humanity[1].new2 = 'name is changed' where @rid= #21:0
```

### Conditions
[Syntax Conditions](http://orientdb.com/docs/2.0/orientdb.wiki/SQL-Where.html)
### Reference
[Regular Expressions](http://www.regular-expressions.info/)

## update record
```sql
> update #50:0 set email='david@naver.com'
```

## expand [LINK]( http://orientdb.com/orientdb-improved-sql-filtering/)
```sql
> select out('Friend')[0] from Profile where name = 'Luca'
```


