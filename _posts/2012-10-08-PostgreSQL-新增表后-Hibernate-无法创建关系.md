---
layout: default
title: PostgreSQL 新增表后 Hibernate 无法创建关系
---
在 PostgreSQL 中新增加一个表之后，总是报错：  
<code>
org.hibernate.exception.SQLGrammarException: could not initialize a collection: [class/field#linenum]  
...  
PSQLException: ERROR: permission denied for relation new_table_just_added  
</code>
  
Well, 虽然不明了中间的机制，但根据[这篇文章](http://www.wwco.com/~wls/blog/2008/07/05/hibernate-schema-update-problems/)中描述的，在 PostgreSQL 中执行下面的语句就能 work 了：  
<code>
GRANT INSERT, SELECT, UPDATE, DELETE, REFERENCES ON new_table TO user_name;  
</code>
