# Control Flow

## A bit about booleans

In clojure everything not ```false``` or ```nil``` is ```true```.

**Things that resolve to ```true```**

```clojure
true
"Hello"
42
[1 2 3 4]
{:key 10}
```

**Things that resolve to ```false```**

```clojure
false
nil
```

## If Statments

### if

```clojure
(if true
  (println "This is always printed")
  (println "This is never printed"))
```

### if-not

```clojure
(if-not true
  (println "This is never printed")
  (println "This is always printed"))
```

### if-let

```clojure
(if-let [x true]
  (println "x = " x)
  (println "x = x"))

(if-let [x nil]
  (println "x has value")
  (println "x is nil"))
```

```clojure
(if-let [x true]
  (println "x = " x))

(if-let [x nil]
  (println "x has value"))
```

if-let is very usefull for interacting with optional data

```clojure
(seq (filter odd? [2 4 6 8]))
(if-let [x (seq (filter odd? [2 4 6 8]))]
  (println "Odd numbers " x)
  (println "x is nil"))

(seq (filter odd? [2 3 4 6 8 9]))
(if-let [x (seq (filter odd? [2 3 4 6 8 9]))]
  (println "Odd numbers " x)
  (println "x is nil"))
```

### Do

Sometimes you want to perform for than one expression in your if statment. Clojure has the do expression is evaluates all enclosed expression and returns the value of the last one. 

```clojure
(println "Print this first")
(println "and then print this")
```

```clojure
(if true
  (println "Print this first")
  (println "and then print this"))
```

```clojure
(if true
  (do 
    (println "Print this first")
    (println "and then print this")))
```

## When Statments

When is a macro for ```if do```, the first parameters is evaluated and if true then all of the other paramiters are executed. 


### when

```clojure
(macroexpand '(when 1 2 3 4))
(macroexpand '(when true 
                (println "Print this first") 
                (println "and then print this")))
```

### when-not

```clojure
(when-not false
  (println "statment 1")
  (println "statment 2"))
  
(macroexpand '(when false 
                (println "statment 1")
                (println "statment 2")))
```

### when-let

```clojure
(when-let [x (seq (filter odd? [1 2 4 5 6 8]))]
  (println "Odd numbers " x)
  (println "And this is also printed"))
  
(when-let [x (seq (filter odd? [2 4 6 8]))]
  (println "Odd numbers " x)
  (println "And this is also printed"))
```

## Cond Case

### Cond

Cond takes in an arbriraty number of expression pairs. The first expression is the true/false conditional, which when true causese the second expression to be evaluated and returned. As soon as cond finds a match it evaluates the epression and returns. 

```clojure
(let [x 15]
	(cond
		(<= x 10) (println "equal to or less than 10")
		(> x 10) (println "greater than 10")))
		
(let [x 5]
	(cond
		(<= x 10) (println "equal to or less than 10")
		(> x 10) (println "greater than 10")))
```

Statments can fall through

```clojure
(let [x 10]
	(cond
		(< x 10) (println "equal to or less than")
		(> x 10) (println "greater than")))
```

Cond short circuits

```clojure
(let [x 5]
	(cond
		(< x 15) (println "less than 15")
		(< x 10) (println "less than 10")))
```

### Case

Basicaly a switch statment

```clojure
(let [s "Mario"]
  (case s
        "Mario" "s = Mario"
        "Bowser" "s = Bowser"
        "no case for s")) ; Optional

(let [s "Toad"]
  (case s
        "Mario" "s = Mario"
        "Bowser" "s = Bowser"
        "no case for s")) ; Optional
```

If none of the cases match and there is no defualt statment then a ```IllegalArgumentException``` is thrown

```
(let [s "Sonic"]
  (case s
        ("Mario" "Bowser" "Toad" "Peach") "s is a Mario character"
        ("Donkey" "Dixie" "Diddy") "s is a Kong"))
```

The test constants can be a list of options

```clojure
(let [s "Diddy"]
  (case s
        ("Mario" "Bowser" "Toad" "Peach") "s is a Mario character"
        ("Donkey" "Dixie" "Diddy") "s is a Kong"
        "default")) ; Optional
```

Test constants can by any type

```clojure
(let [s 10]
  (case s
        ("Mario" "Bowser" "Toad" "Peach") "s is a Mario character"
        ("Donkey" "Dixie" "Diddy") "s is a Kong"
        (1 5 10 12 ) "s is a number"
        "default")) ; Optional
```

## Loop Recur While

