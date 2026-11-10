# Hash Table Analysis Laboratory

## Core goals
Students must implement a hash table that stores key-value pairs using open addressing and quadratic probing.

## Required behaviors
Students must implement:

- insertion with collision handling;
- lookup and retrieval;
- update of existing entries;
- deletion while preserving probe correctness;
- capacity growth and rehashing;
- hash function design;
- complex-key scenarios with many collisions.

## Required analysis
Students should write a short comparison and complexity analysis of:

- average-case insertion, lookup, and removal; All three operations take O(1) time in the average case because they only need to check a few slots.
- best-case and worst-case behavior; The best case is O(1) when the first slot that is checked is the right slot. The worst case is O(n) if a long sequence is needed to account for a crowded table or collisions.
- collision resolution strategies; Chaining can handle collisions by storing multiple entries in the same table index via a linked list. However, this may lead to a slower time complexity. See below.
Open addressing: Handles collision by checking other slots | Linear: checks next slot | Quadratic: checks using quadratic offsets | double hashing: uses another hash function to choose step. 
- load factor and rehashing costs; The load factor is # of stored entries / capacity of the table. As the load factor rises, empty slots are harder to find and probes become longer. When load factor reaches its limit, the table grows and the entries are inserted again. Rehashing takes O(n). Insertion may sometimes become O(n) if the element being inserted causes rehashing, but amortized, it is usually O(1) time.
- open addressing vs. chaining; Open addressing stores directly in table (uses memory efficiently), but load factor must be kept low and deletions need to be handled carefully. Chaining stores multiple entries in the same index, but takes up more space for the chains, and may also cause a slower time complexity.
- how clustering can affect performance. Clustering causes groups of occupied slots to form. Operations that reach these clusters need to make more probes, affecting performance. Quadratic probing reduces the consecutive groups, which is one advantage over linear probing. 

## Big-O expectations
Students should identify and explain the Big-Oh for:

- `insert`: Best and average case is O(1) when slot is found after a few probes, worst case is O(n), when an insertion causes rehashing or a node is being inserted into a chain.
- `remove`: Best and average case is O(1) when the key is found after a few probes, worst case is O(n) if probe sequences needs to examine a lot of slots such as linearly in a chain. Using open addressing, deletion marks the slot as a tombstone and the lookup can continue.
- `get`: Best and average case is O(1) when the key is found quickly, worst case is O(n) when chaining requires linear traversal.
- `update`: Best and average case is O(1) when the key is found quickly, worst case is O(n) when probe sequence is too long and requires linear traversal.
- `rehash`: Rehash involves moving each entry to a new table, which means that it will take O(n) time in the best case and on average.
- `contains`: Best and average case is O(1) if it is an empty slot or is the first element that is searched, worst case is O(n) when multiple probes are needed.

Expected average-case: O(1) for insert, lookup, and update under a reasonable load factor; worst case can degrade to O(n) when many collisions occur or the table becomes badly loaded.
