## Collections

### Strings

In clojure all string are character sequences. Because of this you can apply all functions that work on collections to strings. Additionally Clojure has is own set of string specific functions that are very similar to the standard Java ones found in ```java.lang```.

[clojure.string](https://clojuredocs.org/clojure.string)

```clojure
(require '[clojure.string :as str])

(require '[clojure.string :as str])

(-> "  .LIRpa   ni  yAD    dloc thgIrb  a sAw Ti  "
    str/reverse
    str/trim
    str/lower-case
    (str/replace #"\s+" " ")
    str/capitalize)

;;=> "It was a bright cold day in april"

```

## A small detour

Often you will by applying functions in sucesssion to collections. Thanks to clojures lisp like syntax this can become visually confusing very quickly. Clojure solves this problem with threading macros. 

### Threading Macros

```
(str/capitalize 
	(str/replace 
		(str/lower-case 
			(str/trim 
				(str/reverse "  .LIRpa   ni  yAD    dloc thgIrb  a sAw Ti  "))) 
		#"\s+" 
		" "))
```

vs

```
(-> "  .LIRpa   ni  yAD    dloc thgIrb  a sAw Ti  "
    str/reverse
    str/trim
    str/lower-case
    (str/replace #"\s+" " ")
    str/capitalize)
```

> Walk through all of the indivial steps.

### Thread first (->)

```3 + 1 - 5 + 7``` without threading.


```
(+ (- (+ 3 1) 5) 7)
(+ (- 4 5) 7)
(+ -1 7)
```


```3 + 1 - 5 + 7``` with threading.

```
(-> 1
	(+ 3)
	(- 5)
	(+ 7))
```

```	clojure
(macroexpand-1 
	'(-> 1
		(+ 3)
		(- 5)
		(+ 7)))
```

### Thread last (->>)

```(3 - 1) * 5 + 7``` without threading.


```	clojure
(+ 7 (* 5 (- 3 1)))
(+ 7 (* 5 2))
(+ 7 10)
```

```(3 - 1) * 5 + 7``` with threading.

```	clojure
(->> 1
	(- 3)
	(* 5)
	(+ 7))
```

```	clojure
(macroexpand-1 
	'(->> 1
		(- 3)
		(* 5)
		(+ 7)))
```

### Some String Exercises

```"some string exercises" -> "Some String Exercises"```

```"some" "string" "exercises" -> "Some String Exercises"```

```"some" "string" "exercises" -> "SOME Gnirts Exercises"```

## Back to Collections

### List



### Vector

### Set

### Map
