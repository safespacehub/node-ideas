Here's an example of a node's key-value map.

```
dog -> "Hello dog!"
cat -> "Hello cat!"
bird 
	--> parrot -> "Hello parrot!"
	--> bluejay 
		--> scrubjay ->"Hello scrub jay!"
		--> westernjay -> "Hello western jay!"
```

### Description of Keys
A key is a string. It can point to a value or point to another map, infinitely nesting.

### Getting a key
Looking up a key will return the value it points to, or nil if there is nothing. If the key points to another map, then the whole map is returned.

### Nesting Maps
Nested maps can also be treated as keys, but it will be necessary now to specify an array of keys. Given the example above:

```
Array Format:
GET "bird" "bluejay" "scrubjay"
result: "Hello scrub jay!"

Slash format:
GET "bird/bluejay/westernjay"
result: "Hello western jay!"
```

### Implementation with Objects

There will be an object called Element
```
Element {
	M map[string]Element
	V string
}

func (e Element) IsMap() bool {
	return e.M != nil
}
```

The structure will look like this

```
Master Element (map) -> "Key 1" -> Element String "I am a string!
                     -> "Key 2" -> Element String "I am also a string!"
                     -> "Key 3" -> Element Map -> ...
"
```

A **get** function will search for the element given a key, recursively. If it is not found, a not found element is returned.

A **delete** function will delete the element returning a bool if this has happened.

A **set** function will set a selector and create the necessary maps.