# Mongodb

Introduction


##  Mongodb

#### <i class="icon-file"></i>Why Mongodb Fast

https://stackoverflow.com/questions/9702643/mysql-vs-mongodb-1000-reads

MongoDB isn't as if by magic quicker. If you store a similar knowledge, unionised in essentially a similar fashion, and access it precisely the same approach, then you actually should not expect your results to be wildly totally different. After all, MySQL and MongoDB area unit each GPL, therefore if Mongolian monetary unit had some as if by magic higher IO code in it, then the MySQL team might simply incorporate it into their codebase.

People area unit seeing world MongoDB performance mostly as a result of MongoDB permits you to question in a very totally different manner that's additional smart to your employment.

For example, contemplate a style that persisted plenty of data a couple of difficult entity in a very normalised fashion. this might simply use dozens of tables in MySQL (or any relative db) to store the information in traditional type, with several indexes required to make sure relative integrity between tables.

Now contemplate a similar style with a document store. If all of these connected tables area unit subordinate to the most table (and they usually are), then you would possibly be able to model the information specified the complete entity is hold on in a very single document. In MongoDB you'll be able to store this as one document, in a very single assortment. this is often wherever MongoDB starts sanctionative superior performance.

In MongoDB, to retrieve the complete entity, you have got to perform:

One index search on the gathering (assuming the entity is fetched by id)
Retrieve the contents of 1 info page (the actual binary json document)
So a b-tree search, and a binary page browse. Log(n) + one IOs. If the indexes will reside entirely in memory, then 1 IO.

In MySQL with twenty tables, you have got to perform:

One index search on the basis table (again, forward the entity is fetched by id)
With a clustered index, {we can|we will|we area unit able to} assume that the values for the basis row are within the index
20+ vary lookups (hopefully on associate index) for the entity's pk price
These in all probability are not clustered indexes, therefore the same 20+ knowledge lookups once we tend to work out what the acceptable kid rows area unit.
So the total for mysql, even forward that every one indexes area unit in memory (which is tougher since there area unit twenty times additional of them) is regarding twenty vary lookups.

These vary lookups area unit probably comprised of random IO — totally different tables will certainly reside in numerous spots on disk, associated it's attainable that totally different rows within the same place a similar table for an entity won't be contiguous (depending on however the entity has been updated, etc).

So for this instance, the ultimate tally is regarding twenty times additional IO with MySQL per logical access, compared to MongoDB.

This is however MongoDB will boost performance in some use cases.


#### <i class="icon-folder-open"></i> 


#### <i class="icon-pencil"></i> 


#### <i class="icon-trash"></i> 


#### <i class="icon-hdd"></i>


----------

### Footnotes

[1] 
[2]
