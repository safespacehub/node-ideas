Sub programs are loaded into a node by the key-value system and handled by the super program. The super program will pass in events and also let the sub-program modify the key-value state.

### Example:

This program watches for values to be placed into key "add", adds them to the current sum at key "sum". That's all
```
node = start subnode

node on "set" with key, value:
	if key == "add":
		node set sum [(node get sum) + value]

```

