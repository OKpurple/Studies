```
var j = {
	{
		data : 0
	}
}

j.meta = { "success" }
```
하면

```
j는
{
	{ data : 0 },
	{ meata : "success" }
}
```

### Object.assign
```
var first = { name: "Bob" };
var last = { lastName: "Smith" };

var person = Object.assign(first, last);
console.log(person);

// Output:
// { name: "Bob", lastName: "Smith" } 
```
```
var obj = { person: "Bob Smith"};
var clone = Object.assign({}, obj);
```