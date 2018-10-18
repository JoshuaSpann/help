# SQLite Help
---

## Pretty Printing, Beautifying Tabular Output of `SELECT` Data in a Clean Human-readable way

If you run a `SELECT` statement on a table in MySQL, you get legible output in a table format:

```
mysql> SELECT * FROM myTable;
+----+---------+
| ID | NAME    |
+----+---------+
|  1 | Test    |
|  2 | Example |
|... |...      |
+----+---------+
```

In SQLite, not so much. You have manually tell it to show headers and format the output as columns.

### SQLite 3

```
sqlite> .mode column
sqlite> .headers on
```

Now you should have prettier output:

```
sqlite> select * from myTable;
id   name
---  -----
 1   Test
 2   Example
...  ...
```
Note that any newlines will not be boxed within the confines of the column they appear. Newlines will uglify your text.

---

## Resources

- [How to properly format sqlite shell output?](https://dba.stackexchange.com/questions/40656/how-to-properly-format-sqlite-shell-output)