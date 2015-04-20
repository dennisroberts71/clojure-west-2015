# Clojure Internals

## Which Clojure Expression

``` clojure
(defn m [v]
   {:foo "bar" :baz v})
;; <--   this one  -->
```

## Disclaimer

The talk was a little too involved to take many notes. It will be
useful to go through the Java code later to see what it's doing.

## Tangents

* Consider:
    * clojure.tools.reader
    * clojure.tools.analyzer
* There's no supported API for creating small maps with compile-time
  constant keys as efficiently as the literal syntax.
* A PersistentArrayMap will upgrade itself to a PersistentHashMap as
  new keys are associated with it, but a PersistentHashMap will never
  downgrade itself.
