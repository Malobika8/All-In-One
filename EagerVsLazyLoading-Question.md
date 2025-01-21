# Scenario

### Note that *get()* is eager by default & *load()* lazy.

Consider a class.

When we fetch name and id, it doesn't get list of addresses in the select query while using get(). 
However, when we try to fetch addresses explicitly, the same is selected in the select query. 

### How is get() eager loading in that case? It should ideally fetch everything.
