### .merge method
A great way to merge two hashes is to use the merge method. 

Let's say a student has three tests (a,b and c). The student can retake tests if they want. The scenario below the student's first try is the h1 hash and they decide to re-take test b and c which are the results in h2. 

```
h1 = { a: 90, b: 85, c: 70 }
h2 = { b: 90, c: 67 }
```

Now you want a new hash with the final test scores an easy way to do this is to use the merge method
```
p h1.merge(h2) { |key, old_value, new_value|
  if old_value > new_value
    old_value
  else
    new_value
  end
}
```

The output would be
```
{:a=>90, :b=>90, :c=>70}
```


