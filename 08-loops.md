## `for`

Kotlin's loops are similar to Python's. `for` iterates over anything that is _iterable_ (anything that has an `iterator()` function that provides an `Iterator` object), or anything that is itself an iterator:

```kotlin
val names = listOf("Anne", "Peter", "Jeff")
for (name in names) {
    println(name)
}
```

Note that a `for` loop always implicitly declares a new read-only variable (in this example, `name`) - if the outer scope already contains a variable with the same name, it will be shadowed by the unrelated loop variable. For the same reason, the final value of the loop variable is not accessible after the loop.

You can also create a range with the `..` operator - but beware that unlike Python's `range()`, it _includes_ its endpoint:

```kotlin
for (x in 0..10) println(x) // Prints 0 through 10 (inclusive)
```

If you want to exclude the last value, use `until`:

```kotlin
for (x in 0 until 10) println(x) // Prints 0 through 9
```

You can control the increment with `step`:

```kotlin
for (x in 0 until 10 step 2) println(x) // Prints 0, 2, 4, 6, 8
```

The step value must be positive. If you need to count downwards, use the inclusive `downTo`:

```kotlin
for (x in 10 downTo 0 step 2) println(x) // Prints 10, 8, 6, 4, 2, 0
```

Any of the expressions to the right of `in` in the loops above can also be used outside of loops in order to generate _ranges_ (one type of iterables - this is similar to `xrange()` in Python 2 and `range()` in Python 3), which can be iterated over later or turned into lists:

```kotlin
val numbers = (0..9).toList()
```

If you need to know the index of the current element when you're iterating through something, you can use `withIndex()`, which corresponds to `enumerate()`. It produces a sequence of objects that have got two properties (the index and the value) and two specially-named accessor functions called `component1()` and `component2()`; Kotlin lets you destructure such an object into a declaration:

```kotlin
for ((index, value) in names.withIndex()) {
    println("$index: $value")
}
```


## `while`

The `while` loop is similar to Python (but keep in mind that the condition must be an actual boolean expression, as there's no concept of truthy or falsy values).

```kotlin
var x = 0
while (x < 10) {
    println(x)
    x++ // Same as x += 1
}
```

The loop variable(s), if any, must be declared outside of the `while` loop, and are therefore available for inspection afterwards, at which point they will contain the value(s) that made the loop condition false.


## `continue` and `break`

A plain `continue` or `break` works the same way as in Python: `continue` skips to the next iteration of the innermost containing loop, and `break` stops the loop. However, you can also _label_ your loops and reference the label in the `continue` or `break` statement in order to indicate which loop you want to affect. A label is an identifier followed by `@,` e.g. `outer@` (possibly followed by a space). For example, to generate primes:

```kotlin
outer@ for (n in 2..100) {
    for (d in 2 until n) {
        if (n % d == 0) continue@outer
    }
    println("$n is prime")
}
```

Note that there must be no space between `continue`/`break` and `@`.




---

[← Previous: Collections](collections.html) | [Next: Functions →](functions.html)


---

_This material was written by [Aasmund Eldhuset](https://eldhuset.net/); it is owned by [Khan Academy](https://www.khanacademy.org/) and is licensed for use under [CC BY-NC-SA 3.0 US](https://creativecommons.org/licenses/by-nc-sa/3.0/us/). Please note that this is not a part of Khan Academy's official product offering._