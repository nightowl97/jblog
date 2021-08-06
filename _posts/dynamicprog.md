Title: A first look into Dynamic Programming
Date: 2017-01-19
Category: Programming
Summary: Very simple application of Dynamic Programming
tags: Python, Recursion

Something I didn't know existed until recently
is *Dynamic Programming*. If, like me, you knew
computer scientists use a lot of different
techniques to optimize their algorithms, but
were intimidated by the [Wikipedia article](
https://en.wikipedia.org/wiki/Mathematical_optimization#Major_subfields)
, then this article is for you. Dynamic Programming is
pretty straightforward, even if it sounds
imposing and scary. I've looked around trying to
find why it's called what it is, and the reasons
are mostly because it sounds impressive. We'll
only talk about one of its simplest applications
for now, just to dip our toes in the water.

### A simple recursive algorithm:
If you ever took a programming/CS course, then
at some point you must have learned about
recursion. One of the common first examples you
learn about is this:
```python
    def fib(n):
        if n <= 1:
            return n
        else:
            return fib(n - 1) + fib(n - 2)
```

This function clearly gives you the `n`-th number
in the famous Fibonacci sequence. The first time
you see and understand this, it seems brilliant,
elegant and pretty much perfect. But with a
deeper look, this algorithm is actually going
to turn out to be pretty bad. I'm not going to
talk about whether Recursion is inherently good
or bad. If that's what you're interested in,
I'll just refer you to this [Stack Overflow answer](http://stackoverflow.com/a/3093/4203245).
First, try and run this function for a big enough
n, say 100 for example. It's going to take a very
long time. This is the timing `fib(40)` in a python
2 interpreter:
```python
    fib(40): 102334155
    --- 80.5310001373 seconds ---
```
The time it takes doesn't increase linearly with
n, this algorithm takes exponential time. I'm
sure you can understand if I don't have the
patience to wait for it to calculate a higher
number.

### Here's why it's slow:
As an example, let's take a look at the
recursion tree when we compute `fib(6)`:

![tree](images/tree.jpg)

Each node represents a function call,
and as you can see, we call:
- `fib(4)` Twice
- `fib(3)` 3 times
- `fib(2)` 5 times

In fact every call on the right side of the
tree has already been computed in the left
side, and yet our function will recompute each
call as if it's never seen it before. Imagine
if we had a big number, we'd have to call the
function on the same big numbers multiple times,
calls on small ns will happen at least a few
hundred thousand times. That means a lot of
clock cycles wasted on redundant and completely
unnecessary calculations. If `T(n)` is the time
it takes to calculate the `fib(n)` then:

$$T(n) = T(n - 1) + T(n - 2) = T(n - 2) + T(n - 3) + T(n - 3) + T(n - 4)\ ...$$

And so forth, each step calling T twice, which
means: $T(n) = 2 * 2 * 2 * ... * 2 = 2^n$

This is a time complexity `O(2ⁿ)` hence an
exponential time algorithm. If you can help it,
you should always try to avoid exponential time,
because it is very costly as you can see from the
diagram:

![comp](images/complexity.png)

One last thing. Every time a recursive call
happens, it takes a bit of memory from the call
stack. The amount that is taken is called the
stackframe, and is only freed when the function
returns. In a low level language, deep recursion
will eat up all the memory and cause a stack
overflow. High level languages usually have some
sort of guards against this. In python for
example, you'll cause a maximum recursion depth
error. Sure you can get around these guards, but
they are there for a reason, and you'll rarely
be justified in circumventing them.

### The Dynamic Programming approach:

The second to last 'subfield' in the previously
mentioned [article](https://en.wikipedia.org/wiki/Mathematical_optimization#Major_subfields)
is Dynamic Programming. It says:
> Dynamic programming studies the case in which
the optimization strategy is based on splitting
the problem into smaller subproblems. The
equation that describes the relationship
between these subproblems is called the Bellman
equation.

The splitting-a-problem-into-subproblems part
seems simple enough in principle, but how is
that actually done? The problem with the first
algorithm is the repetition. Each recursive
call is costly, so we should only have to
calculate each $n$-th number once. First thing
that comes to mind is to just save each $fib(n)$
we compute, and cut off the recursion if we ever
call the function on that same $n$ later. Seems
simple right? That's exactly the way we're going
to do it. Whenever the $fib$ function is called,
we will store its result in memory. Later when
it's called with the same argument again,
instead of recursing for a second time (again
and again down to the base case), we just need
to pull the result that we already stored in
memory. This is going to make for a much better
algorithm, and that's because reading from
memory takes constant time, not exponential
time (essentially free). Here's a possible
implementation:
```python
    mem = {}
    def fib(n):
        if n in mem:        # If we've already computed it
            return mem[n]   # then just return that
        if n <= 1:                          # These lines
            return n                        # are still
        else:                               # pretty much
            res = fib(n - 1) + fib(n - 2)   # the same
            mem[n] = res            # Store this result for eventual reuse
            return res              # And now you can return the result.
```
In dynamic programming, we solve all the
subproblems and use their results to solve
our main problem. The "subproblems" in our
case are the all the $fib(k)$s where $k < n$ and
we stored the result of each subproblem in
memory for eventual reuse. It's also pretty
clear that $T(n) = \text{Time for each subproblem} *
\text{Number of subproblems}$. If you try and run this,
you're going to notice a gigantic jump in
performance because this is now a linear time
algorithm O(n). So much so that even I had
the patience to wait for it to calculate the
500-th number:

```python
    fib(500): 139423224561697880139724382870407283950070256587697307264108962948325571622863290691557658876222521294125
    --- 0.00100016593933 seconds ---
```

![ndt](images/ndt.gif)

That was a pretty big number and it did it in roughly 1 millisecond? Hey, that's pretty good!

That's pretty much the idea of dynamic
programming: Recursion + Memory. Our algorithm
worked its way down the tree starting from the
top, but there's also Bottom-up Dynamic
Programming which, as you might expect, works
its way from the bottom. It's also pretty simple
to implement, especially for something as easy
as fibonacci, but that's something I'll let you
do yourself.

### Conclusion

That was a pretty good improvement, but it's
possible to do even better. Our algorithm will
still cause a maximum recursion depth error
for a very big n, and it's possible to make a
logarithmic time O(log n) algorithm using the
closed form for fibonacci numbers, also known
as Binet's formula:

$$\text{fib}(n) = \text{floor}\left(\frac{\phi^n}{\sqrt{5} + \frac{1}{2}}\right)$$ where
$\phi$ is the gloden ratio

You might think this is constant time but due
to the powers in the formula, we need to use
the `math.pow()` function, which is not O(1) like
the usual addition and multiplication operations.
It's also worth noting that this method is
subject to floating point errors during
computations with big numbers, so your results
might be slightly off if you decide to try it
for yourself.

That's about it for now, I hope you learned
something with me today.