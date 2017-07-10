## create Edge
```sql
> create class <edgeName> extends E
```

## delete record
`className`에서 `columnName`인 곳에서 `a`로 시작되는 값들을 지워라.  
특별히 `delete vertex`로 한 것은 이 값들이 단순히  `class`가 아닌`vertex`이기때문에 그렇다.
```sql
> delete vertex from post where content like '%a'
> delete vertex from post where @rid=#41:7
```
## update record
```sql
> update #50:0 set email='david@naver.com'
```


