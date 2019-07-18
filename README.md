# Mongo peoplebase

Here are eight famous people: 

| Id | First Name | Last Name | Year of Birth | Year of Death |
|----|------------|-----------|---------------|---------------|
| 1  | Marilyn    | Monroe    | 1926          | 1962          |
| 2  | Abraham    | Lincoln   | 1809          | 1865          |
| 3  | Nelson     | Mandela   | 1918          | 2013          |
| 4  | Winston    | Churchill | 1874          | 1965          |
| 5  | Bill       | Gates     | 1955          | –             |
| 6  | Charles    | Darwin    | 1809          | 1882          |
| 7  | Pele       | –         | 1940          | –             |
| 8  | Fidel      | Castro    | 1926          | –             |

1. Create a mongo database and a collection called `people` that would store the information presented above.

2. Create a query or a series of queries that would fill the table with the information above. Put the query/queries below:

    ```javascript
    db.people.insert([
            {_id: 1, firstName: 'Marilyn', lastName: 'Monroe', birth: 1926, death: 1962},
            {_id: 2, firstName: 'Abraham', lastName: 'Lincoln', birth: 1809, death: 1865},
    ...     {_id: 3, firstName: 'Nelson', lastName: 'Mandela', birth: 1918, death: 2013},
    ...     {_id: 4, firstName: 'Winston', lastName: 'Churchill', birth: 1874, death: 1965},
    ...     {_id: 5, firstName: 'Bill', lastName: 'Gates', birth: 1955},
    ...     {_id: 6, firstName: 'Charles', lastName: 'Darwin', birth: 1809, death: 1882},
    ...     {_id: 7, firstName: 'Pele', birth: 1940},
    ...     {_id: 8, firstName: 'Fidel', lastName: 'Castro', birth: 1926}])
    ```

3. Create a query that would return everything from the table:

    ```javascript
    db.people.find()
    ```
    
4. Create a query that would return a single row: the person with the ID of 5.

    ```javascript
    db.people.find({_id:5})
    ```

5. Create a query that would return the four people with the following IDs: 1, 3, 7, 8.

    ```javascript
    db.people.find({_id:{$in:[1,3,7,8]}})
    ```

6. Create a query that would return all the people except the person with the ID of 4 (`Winston Churchill`).

    ```javascript
    db.people.find({_id:{$ne:4}})
    ```

7. Create a query that would select the people who were born after 1920:

    ```javascript
    db.people.find({birth:{$gt:1920}})
    ```
    
8. Create a query that would select the living people:

    ```javascript
    db.people.find({death:{$exists:false}})
    ```
    
9. Create a query that would return everyone who has died:

    ```javascript
    db.people.find({death:{$exists:true}})
    ```
    
10. Create a query that would select the people with their first starting with an `M`:

    ```javascript
    db.people.find({firstName:/^M/})
    ```

11. Create a query that would select the people with either their first or last name starting with a `C`:

    ```javascript
    db.people.find({$or:[{firstName:/^С/},{lastName:/^С/}]})
    ```

12. Create a query that would select the people born after 1900 with their last name starting with a `C`:

    ```javascript
    db.people.find({$and:[{birth:{$gt:1900}},{lastName:/^C/}]})
    ```
    
13. Create a query that would select all the people except those whose last name starts with a `C`:

    ```javascript
    db.people.find({lastName:{$not:/^C/}})
    ```
    
14. Create a query that would select the people whose first name starts with a letter that precedes `M` in the English alphabet:

    ```javascript
    db.people.find({lastName:{$lt:'M'}})
    ```
    
15. Create a query that would return all the people sorted by their last name alphabetically:

    ```javascript
    db.people.find().sort({lastName: 1})
    ```

16. Create a query that would return the living people sorted in the reverse alphabetical order by their first name.

    ```javascript
    db.people.find().sort({firstName: -1})
    ```

17. Create a query that would return the people sorted by their year of birth in the descending order, and then (if two or more people share the same year of birth) by their last name alphabetically:

    ```javascript
    db.people.find().sort({birth: -1, lastName:1})
    ```
    
18. Set everyone’s last name to your last name:

    ```javascript
    db.people.updateMany({}, {$set: {lastName: 'myLastName'}})
    ```
    
19. Update the first name of everyone who was born before 1900 to your favorite character’s name:

    ```javascript
    db.people.updateMany({birth:{$lt:1920}}, {$set:{firstName:'anyone'}})
    ```
    
20. Add 1 to both the year of birth and year of death for everyone whose ID is less than 5:

    ```javascript
    db.people.updateMany({_id:{$lt:5}}, {$inc: {birth:1, death: 1}})
    ```

21. Delete from the table everyone who died before 2000:

    ```javascript
    db.people.deleteMany({death: {$lt:2000}})
    ```

22. Delete everyone from the table:

    ```javascript
    db.people.deleteMany({})
    ```
    
Don’t forget to create a pull request.
