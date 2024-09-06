Every node runs a state machine that handles input and output (GET and SET) and runs the sub program as necessary.

## Get Path
1. *Get request received:* GET my-key-value
2. Run sub-program
3. Get value from memory

## Set Path
1. *Set request received* SET my-key-value with "Hello!"
2. Set value in memory
3. Run sub-program

```
// the OFFICIAL instance of node!
// node is basically a string to value map, in memory
// also loads a base program using the same get/set stuff
node = start node

// the following is just an abstraction for TCP/IP
server = start tcp

// this is a handler for inbound "get" messages
server on "get" with key:
	// let the sub program know about the get request
	node notify "get" key

	// get they key from node and return it
	return (node get key)

// a handler for inbound set messages
server on "set" with key, value:
	// intercept program loading
	if key == "load":
		node set key value
		node load value
		return

	// set the key in the node
	node set key, value

	// notify the sub program we are gonna set a key
	node notify "set" key value

```

## Mechanics

### What is a key value map?
A key-value map is an arbitrary key that points to an arbitrary map. It is useful because information can be stored and addressed by a "name".

#### Keys
Key Value maps are tree-like, where a value can be a further collection of key-maps. So the key is just a description of how to get to the value. As an example we can store "banana" at node/memory/fruits.

#### Values
Values are the final endpoint in the tree. It's data type is either string or float.