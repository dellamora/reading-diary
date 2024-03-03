# Part 1: Foundations of Data Systems

### Chapter 1: Reliable, Scalable, and Maintainable Applications

The first chapter was focused on explaining some fundamental ways of thinking about data-intensive applications, what the book will cover, and an overview of what reliability, scalability, and maintainability are.

- **Realiability**: systems should prevent hardware faults, software faults and human error.

- **Scalability**: As the system expands, whether in terms of data volume, traffic volume, or complexity, it's essential to have viable strategies in place to manage and accommodate this growth effectively.

- **Maintainability**: systems should be easey to operate, simple and adaptable.

### Chapter 2: Data Models and Query Languages

Data models are important because they can determine how we think about the problem that we are solving. Applications are built ny layering one data model on top of another.

**SQL**: Based on the relational model proposed by [Edgar F. Codd](https://en.wikipedia.org/wiki/Edgar_F._Codd) the SQL is the best-known data modal today. Data is organized into `tables`, where each relation is an unordered collections of `rows`

**NoSQL**: Have gained popularity because they handle massive amounts of data and high-speed writing better than regular databases. They are also free and open source, making them ideal for unique searches regular databases can't handle, and they offer more freedom in data management.

**ORM: The Object-Relational Mismatch**: Is request just one query because the relavant data are more easy to get it than creating a lot of queries because there are a lot of tables relations and the book cover some examples

(I just got lazy and didn't write more notes about this chapter)

### Chaper 3: Storage and Retrieval

A database needs to do two things: **store data and retrieve data**.
