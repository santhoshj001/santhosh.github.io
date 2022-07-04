---
title: Database views in ROOM 
tags: [Android, Room, DatabaseView]
comments: false
description: Create views into a database.
---

<br>

DatabaseView allows us to encapsulate a query into a class. Room refers to these query-backed classes as views, and they behave the same as simple data objects when used in a DAO.

To create a view, add the `@DatabaseView` annotation to a class. Set the annotation's value to the query that the class should represent.


For example :

```java

@DatabaseView("SELECT user.id, user.name, user.departmentId," +
        "department.name AS departmentName FROM user " +
        "INNER JOIN department ON user.departmentId = department.id")
data class UserDetail(
    val id: Long,
    val name: String?,
    val departmentId: Long,
    val departmentName: String?
)

```

To include this view as part of your app's database, include the views property in your app's @Database annotation:

```java
@Database(entities = [User::class],
          views =[UserDetail::class], version = 1)
abstract class AppDatabase : RoomDatabase() {
    abstract fun userDao(): UserDao
}
```
