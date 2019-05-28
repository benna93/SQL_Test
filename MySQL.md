# SQL

### CONSULTING TABELSTRUCTURES

***What is a primary key?***

>The PRIMARY KEY constraint uniquely identifies each record in a table. Primary keys must contain UNIQUE values, and cannot contain NULL values.
>A table can have only ONE primary key; and in the table, this primary key can consist of single or multiple columns (fields).

Example: 

```
CREATE TABLE  persoon
    (
    id int,
        Voornaam varchar(255) NOT NULL, 
        Achternaam varchar(255) NOT NULL,
        Woonplaats varchar(255),
        Geslacht varchar(1),
        CONSTRAINT PK_persoon PRIMARY KEY (id)
    )
```

ID is the primary key because each field can be identified with it. It shows up as a key in the structure next to the name.

***How many different data types are being used?***

8 in total, we looked it up via the search tab.


***How many rows are there in total?***

115,963 rows.

<br>

### WORKING WITH DATA

Sorting the rows resulted in the following queries:

```
SELECT * FROM `posts|comments|users|votes` ORDER BY `posts|comments|users|votes`.`creation_date` DESC
```

***How many results are there?***

We didn't understand the question, but we think maybe that the number of rows is the anwser. So the anwser is 22306 for posts.


***How long did it take to execute the query?***

Again it depends, ours for example took 0.0631 seconds.

<br>

### CHANGING DATA

Update query after adjusting view_count to 1 and removing the smiley at the end:

```
UPDATE `posts` SET `view_count` = '1', `body` = '<p>You will have to jailbreak your iPhone to password-protect the Mail app. Sorry, there\'s no other way.</p>\r\n' WHERE `posts`.`id` = 23786;   
```

<br>

### INSERTING DATA

**Unclear instructions.**
```
INSERT INTO `posts` (`id`, `post_type_id`, `parent_id`, `accepted_answer_id`, `creation_date`, `score`, `view_count`, `body`, `owner_user_id`, `last_editor_user_id`, `last_edit_date`, `last_activity_date`, `community_owned_date`, `closed_date`, `title`, `tags`) VALUES (NULL, '-128', '2', '1', '2011-08-31 22:58:11', '1', '0', '<p>EWA</p>', '2', '2', '2011-08-31 22:58:11', '2011-08-31 22:58:12', '2019-05-28 00:00:00', '2019-05-23 00:00:00', '', '');
```
<br>

### DELETING DATA

***Why does this post have an ID even though we didn't assign a value to it?***

It has to refer to a unique thing, so it just creates a new number if you add a new row.

What did you get in the confirmation window?
```
DELETE FROM `posts` 
WHERE `posts`.`id` = 24096
```

<br>

### EXPORTING DATABASES
 OK.
<br>

### DELETING ALL DATA FROM TABLE

>Auto-increment allows a unique number to be generated automatically when a new record is inserted into a table.
Often this is the primary key field that we would like to be created automatically every time a new record is inserted.

***What is the value of AUTO_INCREMENT?***

The AUTO_INCREMENT value is 24096. We then emptied the table, which returns the following query:

 ```
 MySQL returned an empty result set (
i.e. zero rows). (Query took 0.0007 seconds.)
 ```

***What is the value now?***

The AUTO_INCREMENT value is still 24096, which we didn't expect it to be.
<br>

### DELETING TABLES

***Browse***
Shows the rows of each table.

***Structure***
Shows the columns of each table.

***Search***
Allows you to search through values of each column.

***Insert***
Allows you to create a new row.

***Empty***
Allows you to truncate(empty out) a complete table.

***Drop***
Allows you to destroy (delete) a complete table.
<br>

### IMPORTING DATABASES AGAIN

Ok.
<br>

### EXPORT-IMPORT WORKFLOW

```
Import has been successfully finished, 
554 queries executed. (stackoverflow (1).sql)
```

<br>
### SEARCHING TABLES

What is the ID of this post?
The ID of reinstalling xcode is 21802.

The query we got:

```
SELECT *  FROM `posts` WHERE `title` 
LIKE 'reinstalling xcode' ORDER BY `id`  DESC
```

**Exercises**

*Flash on OS X Lion*

```
SELECT *  FROM `posts` WHERE `title` 
LIKE 'Flash on OS X Lion' ORDER BY `id`  DESC 
```


*Flash plugin*

```
SELECT * FROM `posts` WHERE `title` 
LIKE '%flash plugin%' ORDER BY `id` DESC
```

*View count*
```
SELECT * FROM `posts` WHERE `view_count` >= 15000 
ORDER BY `id` DESC
```
*Accepted answer ID*

```
SELECT * FROM `posts` WHERE `accepted_answer_id` != 0 
ORDER BY `accepted_answer_id` ASC
```

*Owner ID = Last editor ID*

```
SELECT * FROM `posts` WHERE `owner_user_id` = last_editor_user_id 
ORDER BY `last_editor_user_id` ASC
```

*Owner ID = Last editor ID != 0*

```
SELECT * FROM `posts` WHERE `owner_user_id` = last_editor_user_id 
AND `last_editor_user_id` != 0 
ORDER BY `accepted_answer_id` ASC
```
*10-15*

```
SELECT * FROM `posts` WHERE `score` BETWEEN 10 AND 15 
ORDER BY `accepted_answer_id` ASC
```
You can't put multiple filters in one field.

<br>
### CUSTOM SQL QUERIES

***How many results?***

Using 
```
SELECT * FROM `posts` WHERE `score` > 10 And `score` < 15 
```
we get 193 results.

*Sorting ascending*
```
SELECT * FROM `posts` WHERE `score` > 10 And `score` < 15 
ORDER BY `posts`.`score` ASC
```

*Sorting descending*
```
SELECT * FROM `posts` WHERE `score` > 10 And `score` < 15 
ORDER BY `posts`.`score` DESC
```

*Sorting descending and on view_count*

```
SELECT * FROM `posts` WHERE `score` > 10 And `score` < 15 
ORDER BY `posts`.`score`, `view_count` DESC
```
*1000-2000*
```
SELECT * FROM `posts` WHERE `view_count` > 1000 
AND `view_count` < 2000 
ORDER BY `view_count` DESC
```

*Closed date January 2011*

```
SELECT * FROM `posts` WHERE `closed_date` 
BETWEEN '2011-01-01 00:00:00' 
AND '2011-01-31 23:59:59' 
ORDER BY `view_count` DESC
```

*User 5472*

```
SELECT * FROM `comments` WHERE `id` = 5472 AND `score` > 0 
ORDER BY Browse`view_count` DESC
```

*Flash of iPad*

```
SELECT *  FROM `posts` WHERE `title` LIKE '%flash%' OR 'ipad' 
ORDER BY `view_count`  DESC
```

*San Francisco*


```
SELECT * FROM `users` WHERE `location` LIKE 'san francisco'
```

*Average view_count as integer*
```
SELECT FLOOR(AVG(view_count)) FROM `posts`
```
*Average view_count of posts with accepted_answer_id*
```
SELECT FLOOR(AVG(view_count)) FROM `posts` WHERE `accepted_answer_id` != 0
```
*Creation date 2011*
```
SELECT *  FROM `posts` WHERE `creation_date` 
BETWEEN '2011-01-01 00:00:00' AND '2011-12-31 23:59:59' 
ORDER BY `view_count`  DESC
```

