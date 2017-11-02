# Intro

Python has probably the best looping syntax I've encountered.

    for x in iterable:
        do_something(x)

It powers our generator expressions:

    (do_something(x) for x in iterable if filter_function(x))

Combined with some of our key built-ins, it allows us to replace messy syntax

    i = 0
    for x in iterable:
        do_something(i, x)
        i += 1

    for i in range(len(iterable1)):
        do_something(iterable1[i], iterable2[i])

with a much nicer:

    for i, x in enumerate(iterable):
        do_something(i, x)
    
    for x, y in zip(iterable1, iterable2):
        do_something(x, y)

But with all of this power, there's more we can do:

    import itertools

Itertools is full of functional building blocks for iterating.

Before you dip your toe into itertools: remember that many of these can be
replaced with generator expressions in many cases.

So let's look at some of the fun stuff:

Sometimes you want to do something with `range` but infinitely. `count` has
you covered.

    for x in count():
        do_something()

Additionally, count can do much of the tricks you can do with `range`:

    for x in count(1, 5):
        print(x)

    for x in count(-1, -1):
        print(x)

A controversial opinion I've come across is to hide
`while True` loops behind infinite iterators:

    for _ in count():
        do_something()

Next, let's talk about chain.

If you've ever needed to iterate over multiple lists, this is the function for
you.

    list1 = [1, 2, 3]
    list2 = [4, 5, 6]
    for x in chain(list1, list2):
        print(x)

Or maybe you have a multidimensional array you'd like the individual items of:

    array = [[1, 2, 3], [4, 5, 6]]
    for x in chain.from_iterable(array):
        print(x)

Next up `cycle` and `repeat`.

    for x in cycle([1, 2, 3]):
        print(x)

    for x in repeat(500):
        print(x)

These are for repetitive iterables. The documentation for repeat suggests it
for use in zip to create an invariant part of a tuple, or map to pass the same
parameter.

Cycle is like repeat, but repeats all elements of an iterable. Note that it
does so by storing each result of the intial iterable so can become quite
memory intensive.

Next is one I wish I'd have known when solving some problems with video game
development: `combinations`.

    for x, y in combinations([1, 2, 3, 1], 2):
        print(x, y)

Use it to get every possible combination for a given number of options in
another iterable, sorted lexographically without repetition.

Used on a list of game objects you can easily check collisions.

The last itertool I'm going to show off is product: Get a cartesian product of
two iterables.

    for x in product([1, 2, 3], [4, 5, 6]):
        print(x)

Back to the same example as before: collision detection, this is how you would
get the combinations for multiple groups.
