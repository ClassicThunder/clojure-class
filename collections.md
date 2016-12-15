## Collections### StringsIn Clojure all string are character sequences. Because of this you can apply all functions that work on collections to strings. Additionally Clojure has is own set of string specific functions that are very similar to the standard Java ones found in ```java.lang```.[clojure.string](https://clojuredocs.org/clojure.string)```clojure(require '[clojure.string :as str])(require '[clojure.string :as str])(-> "  .LIRpa   ni  yAD    dloc thgIrb  a sAw Ti  "    str/reverse    str/trim    str/lower-case    (str/replace #"\s+" " ")    str/capitalize);;=> "It was a bright cold day in april"```## A small detourOften you will by applying functions in succession to collections. Thanks to clojures lisp like syntax this can become visually confusing very quickly. Clojure solves this problem with threading macros. ### Threading Macros```(str/capitalize 	(str/replace 		(str/lower-case 			(str/trim 				(str/reverse "  .LIRpa   ni  yAD    dloc thgIrb  a sAw Ti  "))) 		#"\s+" 		" "))```vs```(-> "  .LIRpa   ni  yAD    dloc thgIrb  a sAw Ti  "    str/reverse    str/trim    str/lower-case    (str/replace #"\s+" " ")    str/capitalize)```> Walk through all of the induvial steps.### Thread first (->)```3 + 1 - 5 + 7``` without threading.```(+ (- (+ 3 1) 5) 7)(+ (- 4 5) 7)(+ -1 7)``````3 + 1 - 5 + 7``` with threading.```(-> 1	(+ 3)	(- 5)	(+ 7))``````	clojure(macroexpand-1 	'(-> 1		(+ 3)		(- 5)		(+ 7)))```### Thread last (->>)```(3 - 1) * 5 + 7``` without threading.```	clojure(+ 7 (* 5 (- 3 1)))(+ 7 (* 5 2))(+ 7 10)``````(3 - 1) * 5 + 7``` with threading.```	clojure(->> 1	(- 3)	(* 5)	(+ 7))``````	clojure(macroexpand-1 	'(->> 1		(- 3)		(* 5)		(+ 7)))```### Some String ExercisesTry to accomplish the below string transformation in one threading macro.* ```"some string exercises"``` -> ```"Some String Exercises"```
* ```"string"``` -> ```"Gnirts"```
* ```"some string exercises "``` -> ```"SOME-STRING_EXERCISES+"```## Back to Collections### Lists ```()``` and Vectors ```[]```

* Lists are backed by a linked list
* Vectors are back by an arrayCreating a list```clojure(let [x '(1 2 3 4)]
  x)
```

```clojure
(let [x (list 1 2 3 4)]
  x)```Creating a vector

```clojure
(let [x [1 2 3 4]]
  x)
```

```clojure
(let [x (vector 1 2 3 4)]
  x)
```

#### Conj

Conj adds to the front of lists

```clojure
(conj `(1 2 3 4) "boo")
```

Conj adds to the rear of vectors

```clojure
(conj [1 2 3 4] "boo")
```Due to immutable state and sequences many of the benifits of linked lists are not realized. Because of this vectors are perfered almost universially. 

Only when generating code in macro's are lists perfered.### Set ```#{}```

Sets force uniqueness 

```clojure
(hash-set :a :b :c :d)
```

```clojure
(sorted-set :a :b :c :d)
```

Set literal

```clojure
#{:a :b :c :d}
#{4 2 1 3}
#{4 2 1 3 4 3} ; IllegalArgumentException Duplicate key:
```

You can also convert any other sequence to a set using the set function

```clojure
(set [3 2 1 2 1 2 3]) ; Hash-set is used by default
```

Interacting with sets

```clojure
(def s #{:d :a :b :e :c})
(disj s :d) ; Remeber state can't change so it returns a copy
(contains? s :b)
(get s :a)
```

Sets can treated as functions for a shorthand replacement of the get function

```clojure
(#{4 2 1 3} 4)
(#{4 2 1 3} 5)
```### Map ```{}```Maps are Clojures bread and butter data structure.   Map literals. Hash maps are the default.```clojure{:language "Clojure"  :creator "Rich Hickey" :repl "http://www.tryclj.com/"  :docs "https://clojuredocs.org/"}```You can also explicitly specify the backing data structure.```clojure(hash-map	:language "Clojure" 	:creator "Rich Hickey"	:repl "http://www.tryclj.com/" 	:docs "https://clojuredocs.org/")``````clojure(sorted-map 	:language "Clojure" 	:creator "Rich Hickey"	:repl "http://www.tryclj.com/" 	:docs "https://clojuredocs.org/")``````clojure(array-map 	:language "Clojure" 	:creator "Rich Hickey"	:repl "http://www.tryclj.com/" 	:docs "https://clojuredocs.org/")```Maps must be key/value pairs.```clojure{:language "Clojure" :creator}``` Commonly used modification functions.(def m {:language "Clojure"         :creator "Rich Hickey"        :repl "http://www.tryclj.com/"         :docs "https://clojuredocs.org/"})```clojure(assoc m :t "leiningen") ```dissoc```clojure```merge```clojure```