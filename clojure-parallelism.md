# Clojure Parallelism

Exploring parallelism beyond futures.

The speaker wrote a parallelism library called `claypoole`, which
might be something useful to explore. Although, I don't know if we can
use it at iPlant or not.

## Running Example

```clojure
(defn crps
 "Continuous Rank Probability Score"
 [precip-observed precip-model]
 (->> (map single-crps precip-observed precip-model)
      (reduce +)
      ;;
      (* @scale)))
```

## Future

### Limitations of Future

You'll have problems if:

* Your tasks are small compared to the overhead
* You want to control the number of concurrent threads.
* you expect exceptions to work normally.

## PMAP

* Lazy and needs to be driven.
* Generates threads as needed.
    * Beware of simultaneous pmaps.
    * It's wacky when there's chunking.
* Runs roughly ncpus + 3 tasks.
    * A long-running task will stall it.

### Limitations

* All limitations of futures.

## core.async

* Uses CSP channels and coroutines.
    * Looks kind of like Go.
    * Reads like one flow: avoid callback hell.
    * Uses cooperative multithreading.
    * Backed by a fixed-size thread pool.
* Mostly for concurrentcy, not parallelism
    * You shouldn't block too many of its threads.
    * Easy to wait on other work.
    * Use it to interact with worker threads.
* Parallelism using `pipeline`
    * Runs a transducer between two channels with parallelism `n`
    * Also `pipeline-async` and `pipeline-blocking`
* Exceptions will kill your coroutines.

## claypoole

https://github.com/TheClimateCorporation/claypoole

* Uses thread pools to control parallelism.
* Can auto-manage thread pools.
* Tries to get things done fast.
    * Default is eager.
    * Ouptut blocks on incomplete tasks.
* Doesn't stall on slow tasks.
* Streaming seqs can be chained.
* `future`, `pmap`, `pfor`
* Unordered functions.
* Lazy versions of these functions are available.
* Exceptions are re-thrown correctly.
* Eliminates chunking.
* Priorities are available.

## Reducers

http://clojure.org/reducers

## Tesser

https://github.com/aphyr/tesser

## Questions

How might we use some of these libraries at iPlant?
