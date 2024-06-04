# Hashing 
The aim of hashing is to reduce the universe (all keys we are trying to insert) down to a size we can manage. We do this through using a hash function, which maps keys onto the reduced universe. There is a notable issue with most hash functions though. It is likely, depending on the hash function, that two keys we are inserting will generate the same hash, and be inserted into our hash table at the same index causing a collision

# Collision resolution
## Chaining
Chaining is a form of collision resolution that maintains a linked list at every position of our hash table. When we insert to our hash table now, we will append to the linked list that is at our hash position, which gets rid of collisions. However, it will increase the time complexity as we will have to search through the linked list in linear time to find our item (time for searching can be improved using a different data structure). 

## Open Addressing (Probing)
Open addressing involves storing all our items in the table directly. To do so, we use a technique called probing. Probing means that when we hash to a position and there is already an item stored there, we search for another free spot in the hash table to insert into. 

Caution must be taken when deleting using open addressing, as simply deleting an item may make items unreachable if the deleted item was placed there via probing. Instead, we can mark an item as *deleted* so when we are searching for an item in the table we just skip over it.

An important fact to consider when using open addressing is the load factor. The load factor is the (number of items in table)/(table_size). As our load factor increases, so will the amount of probing we need to do, worsening the time complexity of inserting and searching. A common strategy is to resize the hash table when the load factor reaches a certain threshold (often 0.5, but varies depending on probing technique) so we will not have to probe as much as there will be more open positions.

### Linear probing
Linear probing is a probing technique that searches linearly from our original hash position until we find another open spot to insert into. In theory, linear probing performs slowly due to *primary clustering* which means that a cluster of keys will form together as we constantly probe and insert them next to one another. This worsens the time complexity as we will have to probe through this cluster to find an item in the hash table

### Quadratic probing
Quadratic probing is similar to linear probing, but instead of searching linearly for another open spot we search quadratically. This technique is prone to *secondary clustering* as keys with the same hash value will always end up probing the same elements.

### Double hashing
In double hashing, we use a second hash function to determine the distance between probed elements. This avoids clustering, however can sometimes be less efficient in practice as we have to compute 2 hash functions\
