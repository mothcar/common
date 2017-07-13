## create Edge
```sql
> create class <edgeName> extends E
```

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


