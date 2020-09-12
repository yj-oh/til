# Querydsl 표현식
```text
//Standard              Alternative

expr isNotNull          expr is not(null)
expr isNull             expr is null
expr eq "Ben"           expr === "Ben"
expr ne "Ben"           expr !== "Ben"
expr append "X"         expr + "X"
expr isEmpty            expr is empty
expr isNotEmpty         expr not empty

// boolean
left and right          left && right
left or right           left || right
expr not                !expr

// comparison
expr lt 5               expr < 5
expr loe 5              expr <= 5
expr gt 5               expr > 5
expr goe 5              expr >= 5
expr notBetween(2,6)    expr not between (2,6)
expr negate             -expr

// numeric
expr add 3              expr + 3
expr subtract 3         expr - 3
expr divide 3           expr / 3
expr multiply 3         expr * 3
expr mod 5              expr % 5

// collection
list.get(0)             list(0)
map.get("X")            map("X")
```

##### * Reference : http://www.querydsl.com/static/querydsl/4.1.3/reference/html_single/#d0e1933
