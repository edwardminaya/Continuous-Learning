### .mapping method
For a long time I had trouble indexing over a hash to pull out a certain attribute and found it tedious to write the code.

For example:
```
people = [
  {
    first_name: "John",
    last_name: "Doe"
  },
  {
    first_name: "Jane",
    last_name: "Doe
  }
]
```

To pull out the first name of each person I would have used the following:
```
first_names_only = []
i = 0
while i < people.length
  first_names_only << people[i]["first_name"]
  i += 1
end
```

Using the mapping method I can write fewer lines of code
```
first_names_only = people.map {|x| x["first_name"]}
```
