---
tirle: SQL 增删改查语句
date: 2018-04-30 20:51:45
tags: SQL
---

## 查询

```sql
'SELECT *(项目名) FROM posts WHERE id=xxx';

字符串拼接
'SELECT id, avatar, name, gender, birthday FROM users WHERE id=' . $id;

'SELECT posts.id, posts.title, users.nickname, categories.name, posts.created, posts.status FROM posts LEFT JOIN users ON posts.user_id = users.id LEFT JOIN categories ON posts.category_id = categories.id LIMIT ' . $offset . ', ' . $pageSize

'SELECT p.id, p.title, p.brief, p.time, p.uid, u.avatar, u.name ' + 'FROM posts AS p LEFT JOIN users AS u ON p.uid = u.id ORDER BY p.time DESC ' + 'LIMIT ?,?'
// 倒序sql语句
```

## 增加

```sql
'INSERT INTO users (KEY1, KEY2, ...) VALUES(VAL1, VAL2, ...)';

字符串拼接
'INSERT INTO users (' . implode(',', $keys) . ') VALUES("' . implode('","', $values) . '")';
```

## 删除

```sql
'DELETE FROM users WHERE id=xxx'; // 删一个
'DELETE FROM users WHERE id IN (1,4,32)'; // 删多个

字符串拼接
'DELETE FROM categories WHERE id IN (' . $_GET['ids'] .')';
```

## 改动

```sql
'UPDATE users SET key1=xxx, key2=xxx, key3=xxx, key4=xxx WHERE id=xxx';

字符串拼接
'UPDATE users SET ' . $str . ' WHERE id=' . $id;
```

