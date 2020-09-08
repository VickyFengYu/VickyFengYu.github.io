# Design eCommerce Website

Building an eCommerce website requires things like database design, system availability, concurrency consideration and so on so forth. All of them are extremely important in today’s distributed systems.


## eCommerce model
how would you design the basic data structure of an eCommerce website? And what about the database schema?

Let’s focus on the product. In the simplest scenario, we need three major objects: _Product_, _User_ and _Order_.

_Product_ defines the basic model for a product in the shopping cart. Some important fields include price, the amount left, name, description, and the category. Category can be tricky here. Of course you can make it a string field in the SQL database, but a better approach is to have a _Category_ table that contains category ID, name and maybe other information. So the each product can keep a category ID.

_Order_ stores information  about all the orders made by users. So each row contains the  product ID, user ID, amount, timestamp, status and so on. So when a user proceeds to checkout, we aggregate all the entries associated with this user to display in the shopping cart (of course we should filter out items that were bought in the past).


## NoSQL in eCommerce

In the above analysis, we are using a [relational database](https://en.wikipedia.org/wiki/Relational_database) like MySQL. In reality, [NoSQL](https://en.wikipedia.org/wiki/NoSQL) database can be a better choice for eCommerce website sometimes.

Why will NoSQL be (slightly) higher during this case? Let’s use _Product_ model as associate degree example. Suppose we have a tendency to square measure commercialism books. A product has class book and plenty of attributes like author, publish date, version, the quantity of pages etc. and this SQL table could have twenty columns. That’s fine.

And now, we have a tendency to additionally wish to sell laptops. thus a product ought to additionally store attributes of a laptop computer together with brand, size, color etc.. As you'll imagine, with additional classes introduced, the _Product_ table will have plenty of columns. If every class has ten attributes in average, it’s gonna be one hundred columns with solely ten classes supported!

However, for NoSQL information like [MongoDB](https://en.wikipedia.org/wiki/MongoDB), a good advantage is that it supports vast variety “columns” like this. every row will have an outsized variety columns however not all of them square measure set. It’s like storing JSON object as a row (in reality, MongoDB is mistreatment one thing terribly similar referred to as [BSON](https://en.wikipedia.org/wiki/BSON)). As a result, we will simply store all those attributes (columns) of a product in a very single row, that is strictly what NoSQL information sensible at.

For more information, have a look at [ Why Mongodb Fast](https://vickyfengyu.github.io/vicky.github.io/SysDesignSecond)


## Concurrency

let’s say there’s just one book left within the store and 2 individuals expire at the same time. with none concurrency mechanism, it’s completely potential that each have bought it with success. however does one attain concurrency in eCommerce websites?

Let’s analyze this step by step. From what we have a tendency to learned from OS categories, we all know that lock is that the commonest technique to safeguard common resources. Suppose each user A and B wish to shop for identical book. What we will do is once A fetches the info concerning this book, place a lock on this row so nobody else will access it. Once A finishes the acquisition (decrease the quantity left), we have a tendency to unharness the lock so B will access the info. identical approach ought to apply for all the resources and this will solve the matter whole.

The higher than answer is termed [pessimistic concurrency control](https://en.wikipedia.org/wiki/Concurrency_control#Concurrency_control_mechanisms). though it prevents all the conflicts caused by concurrency, the draw back is that it’s expensive. Obviously, for each information access we want to form and unharness a lock, which can be spare most of the time.


## Concurrency (continued)

we know that one approach is to put a lock on the row whenever somebody accesses the resource (book) in order that at the most one person will read/write the info at a time. the answer is named [pessimistic concurrency control](https://en.wikipedia.org/wiki/Concurrency_control#Concurrency_control_mechanisms). though the approach will forestall 2 folks accessing a similar information at the same time, inserting locks is kind of expensive. 

[Optimistic concurrency control](https://en.wikipedia.org/wiki/Optimistic_concurrency_control) is otherwise to support concurrency. the thought is incredibly straightforward – rather than victimization locks, every process/thread will access information freely. However, before committing changes, every dealing ought to check if the info has a similar state because it did after you last browse it. In alternative words, you check the info within the starting of the dealing and check once more before committing to check if they're still a similar.

If the info hasn’t been changed, you'll be able to safely commit it. Otherwise, roll back and check out once more till there’s no conflict. It’s vital to match the 2 approaches here. For OCC (Optimistic concurrency control), apparently it’s a lot of economical to read/write information unless there area unit conflicts. thereupon in mind, for systems that area unit unlikely to possess conflicts, OCC may be a higher possibility. However, once resources area unit often accessed by multiple purchasers, restarting dealing becomes expensive in OCC and it’s higher to put locks in every dealing (PCC).

In applications like Amazon, there area unit such a lot of product that it’s not that frequent to possess multiple folks accessing a similar product at the same time. As a result, OCC may be a better option.

For more information, have a look at 
[Concurrency Java](https://vickyfengyu.github.io/vicky.github.io/SysDesignThird)


## Availability in eCommerce

It’s an enormous loss if Amazon web site is down for one minute. to attain high convenience in distributed systems, the simplest manner is to possess lots of or thousands of replicas so you'll tolerate several failures. However, it’s value to notice here that convenience and consistency go hand in hand.

If you have got several replicas, it’s undoubtedly tougher to ensure that every reproduction has a similar information. On the flip facet, if you wish to attain high consistency, you’d higher have fewer replicas, therefore the system is liable to failure.

The idea here is not making an attempt to attain each. Instead, supported the character of the merchandise, you must be ready to create the trade-off. For AN eCommerce web site, latency and down time typically means that losing revenue, which may be an enormous range typically. As a result, we'd care additional concerning convenience than consistency. The latter are often improved through alternative approaches.


## Consistency in eCommerce

Given that we've a whole lot or thousands of replicas, however would you guarantee that every reproduction keeps a similar data? to elucidate the matter thoroughly, suppose information D is replicated in multiple servers. once a method is making an attempt to update D to D1, it starts from one server and follows a selected order to propagate the changes. At a similar time, another method is making an attempt to update D to D2 and it should begin from another server. As a result, some servers having information D1 and a few D2.

### Eventual consistency

Let’s take [Amazon’s Dynamo](https://en.wikipedia.org/wiki/Dynamo_(storage_system)) as Associate in Nursing example. Basically, it’s attainable that every duplicate holds completely different versions of the information at a specific time. therefore once the consumer scan the information, it should get multiple versions. At now, the consumer (instead of the database) is accountable to resolve all the conflicts and update them back to the server.

You might surprise however will the consumer resolve those conflicts. It’s principally a product call. Take the handcart as Associate in Nursing example, it’s vital to not lose any additions since losing additions suggests that losing revenue. therefore once facing completely different values, the consumer will simply opt for the one with most things. This is Eventual Consistency. For more information, have a look at 
[Consistency in E-Commerce](https://vickyfengyu.github.io/vicky.github.io/SystemConsistency)

----------

### Footnotes

[1] http://blog.gainlo.co/index.php/2016/08/22/design-ecommerce-website-part/

[2] http://blog.gainlo.co/index.php/2016/08/28/design-ecommerce-website-part-ii/
