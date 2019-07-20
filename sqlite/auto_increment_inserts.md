# SQLite Help
---

## Auto-Incrementing on Record Insert
You do not need to use the `auto_increment` keyword, as sqlite does this already with a rowid. If you have an int primary key field that does so, it will link to rowid anyway.

If you need the 'auto-incremented' id field, select the `rowid` field. Each table has a `rowid` field.

`select rowid, id, name from myTable;`

---

## Resources
- [SQLite AUTOINCREMENT : Why You Should Avoid Using It](http://www.sqlitetutorial.net/sqlite-autoincrement/)