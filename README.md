# What's in here

*TLDR*: these are just a series of experiments that I'm doing in order to understand how to solve in this case the problem of creating a very, very simple store in several languages, functional and imperative.

The key idea is to create a store that can have O(1) characteristics for read and write. 
The stores use a map as in memory data structure and are backed by NDJSON files.
The stores can either be monomorphic, meaning one single type of JSON structure or polymorphic
Such as there could be different JSON structures. Note that in the previous sentence "monomorphic"
is a misnomer, because a JSON store can store whatever structure is in the JSON string. Possibly
a better characterization would be single-key or multi-key, because in order to create a store that
can be efficiently accessed in O(1) time, you need a key. You need then to specify the key when
creating the store, that's all there is. For the case of multiple keys, you need to pass-in to
the constructors, either an array of possible keys, or a "key extractor" which is a small function
that recognizes the first key it finds among a set of keys in a JSON object.

Do not look for something fancy in here, but rather it's a language exercise. If you're looking
for a serious key value pair store, look for something like LMDB which is proven, mature, uses
B-trees, memory mapped files and a host of other very useful mechanisms. 