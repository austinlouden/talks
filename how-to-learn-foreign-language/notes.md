Abstract:

Composable Caching in Swift


Consider what it means to be a cache. You need to be able to 
(1) associate a key with a value and 
(2) get some value given a key if such a value exists. 
That's basically it. Caches tend to appear in layers. In a CPU, memory reads check L1, then L2, then L3, then RAM. When we want to load an image, we first check RAM, then disk, and finally network. 

In a mobile app, if you don't nail your cache code, your users will suffer. Excessive networking causes both battery and data-plan drain. We can help ensure a clean correct implementation by combining caches. Given two caches A and B, A `on-top-of` B means first check A, fallthrough to B, then write back to A. Now we can define a monoid for caches. Monoids imply easy composition. Easy composition means reasoning about our code becomes easy.

Such an abstraction isn't possible to express both statically and generically in languages like Objective-C and Java, but we can with Swift's strong type system. The caching library Carlos provides the foundation upon which we can build prefetching and other useful transformations. In our app, adopting such a system simplified our codebase: Caches became reusable legos. But the complexity doesn't just all go away, it's just hidden. When an abstraction is so nice, it's tempting to think of the actual caches and cache glue as black-boxes. One problem we ran into was a reference cycle that led to large bitmaps leaking and phones running out of memory. It's important to actually think about the implementation details in detail, since these are your building blocks for the rest of the system. When your building blocks are stable, your building is stable.

Caching and prefetching are necessary for mobile apps. In this talk, I will explain how to think about caches as monoids, how a monoidal caching system can simplify our jobs as software engineers, and what real-world problems we ran into when putting such a system into production.



Story:

Photos app ->
Needs caching ->
Ad hoc caching is messy ->
Let's manage the complexity ->
Too specific ->
Abstraction ->
Cache protocol ->
Implementations of protocol ->
Networking needs to give images ->
Transformations ->
Return value for map? ->
Lambda cache / Basic cache ->
Map still needs another contra-transform ->
Because it needs both it's a profunctor ->
Too slow to convert, need async map ->
Key transforms are contravariant functors ->
(need transition)
Reusing inflight requests ->
How do we reuse across disk and network ->
Cache layering ->
It's monoid ->
Monoid means composable ->
Legos ->
Transformations ons legos (for any legos) ->
Simple(r) client-side caching ->
Simpler?, you still need the imperative core! ->
Bugs interfacing with native libs -> (networking) ->
Bugs in the core of the library -> (futures) ->
Better summary





Don't summarize so fast

Photos

===

Downloading from network: 30sec
Disk: 1sec
Ram: 1ms

Have a picture; have a diagram;

===

Thanks p for sponsoring. Thanks for m

===

Maybe remove showing the progress of fetch

Also videos and comments and...

===

Consider ripping out lambdacache and not-so-simple

It's important to be generic

Go slower on the `set` possibly

Consider making squares and circls

It's not that the actual caches changes, it's that when you call it, the functions

===

Picture (maybe an animation)
showing where the new request comes in (loadDataSafley)

===

`onTopOf` is too fast
Simplify the type signature of `onTopOf`
don't need `e in` in the `onTopOf` come from

===

Insert carlos callout

===

We're staying in the real problems section
Real problem #2

===

When using some library and you call `.magic`, you can't assume that everything is amazing in that function

===

Now that we've fixed the bugs...

===

Real example? loading the images (a diagram)
SUMMARY at the end


1. see if we have the images
2. load them from dictionary?
3. load them from...
...
7. Fetch from database

New feature (users can upload videso)

Show how crappy the world is, then show the not crappy

At the end so we want to load anything?

1.dd
2. sad
3. asd
