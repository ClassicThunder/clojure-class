## Clojure Traning Syllabus

* Getting Started
 * Setup
 * REPL * Hello World* [Terminology](terminology.md)
 * Expressions 
 * Functions
 * Bindings
* [Bindings](bindings.md)
 * Def
 * Let
 * Scoping
* [Control Flow](controlflow.md)
 * Booleans
 * if, do, when, cond, case, loop, recur, and while
 * *Excersize*
* [Collections](collections.md)
 * strings, list, vector, set, map 
 * *Excersize*
* Sequences
 * realized, lazy
 * *Excersize*
* Functions 
 * defn, anonymous functions, inline, clojures 
 * *Excersize*
* Map/Reduce
 * *Excersize*
* Clojure @ COF
 * Summary of where we are in terms of frameworks used and current problems we face
 * *Excersize*
  
Notes

1. Control Flow - Map/Reduce is modeled after [Daniel Higginbotham's class](https://github.kdc.capitalone.com/RDT/clojure-training) and [Clojure by Example](https://kimh.github.io/clojure-by-example/#count). For each section there will be a walk through of the tools the language provides and then a few small excersizes to apply them.

2. Map/reduce is difficult but vital to leveraging the language properly. Probably best to hammer this in at the expense of other oppertunities.

3. Put the things learned earlier into practice. Load up the refapp make it do something using some dependencies and write some tests.4. Things that could be added but we probably don't have time for Atoms/Vars, Deftype/Defrecord, Macros.## MAC Getting StartedNeed to have your command line proxy configured. ```brew install leiningenlein new testprojlein new app testprojcd testprojatom .```* Brief walkthrough of the project and the files it contains. * Brief walkthrough of leiningen and the project.clj file. Draw comparisons to Maven.## Windows Getting Started

[Lein Download](http://leiningen-win-installer.djpowell.net/)## Hello World```clojurelein repl (println "Hello, world!")```