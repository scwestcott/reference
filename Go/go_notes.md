# Go

## Maps: map[string]int

- [string]: key type  
- int: value type

```
var := map[string]int { "key": 0 } // Composite literal assignment.
var := make(map[float64]int, 8) // Capacity: 8 (optional)
```

Maps are collections of key:value pairs, where the key can be nearly any type.
Similar collections in other language go by other names: dictionaries in Python,
hashes in Ruby, objects in JavaScript, and associative arrays in PHP.

- Maps share the same underlying data when assigned or passed to functions (like a slice; unlike an array)

### Map Examples

```
// Composite literal assignment.
temperature := map[string]int{
	"Earth": 15,
	"Mars": -65,
}

// Comma okay syntax.
if moon, ok := temperature["Moon"]; ok {
	fmt.Printf("%v: On average the moon is %vC\n", ok, moon)
} else {
	fmt.Printf("%v: Moon, where art thou?\n", ok)
}

// Use a map to make a set. (Warning: map keys have arbitrary order. Convert to slice to order.)
temperatures := []float64{
	-28.0, 32.0, -31.0, -29.0, -23.0, -29.0, -28.0, -33.0,
}

set := make(map[float64]bool)

for _, t := range temperatures {
	set[t] = true
}

// Convert to slice for sorting.
unique := make([]float64, 0, len(set))
for t := range set {
	unique = append(unique, t)
}
sort.Float64s(unique)
```
