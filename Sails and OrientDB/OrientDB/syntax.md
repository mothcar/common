## create Edge
```sql
> create class <edgeName> extends E
```

## delete record
`className`에서 `columnName`인 곳에서 `a`로 시작되는 값들을 지워라.  
특별히 `delete vertex`로 한 것은 이 값들중에 `vertex`가 있어서 그렇다.
```sql
> delete vertex from <yourClass> where <columnName> like '%a'
```

