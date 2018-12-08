#1) books

TODO: effective modern c++ 

TODO: professional c++

#2) leetcode.com
TODO: https://leetcode.com/problemset/top-100-liked-questions/

#3) https://practice.geeksforgeeks.org/tracks/CPP/

DONE: tried some tasks, practice looks like not the best option

TODO: check topics to be prepared (theory)


#4) https://www.tutorialcup.com/cplusplus-interview-questions

TODO: decent list of C++ interview questions


#5) https://isocpp.org

TODO: https://isocpp.org/faq ; decent FAQ; go trough

TODO: http://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines ; nice guidelines; useful in daily work


#6) https://encelo.github.io/notes.html

TODO: go trough list of topics & learn

TODO: design patterns

#7) Code/ practice questions

Cpp11 features

Move/Templates/5 special funcs/example class code from scratch

multithreading / stream questions


#8) Topics to cover :
- void* + dynamic cast

- order of initialisation

- concurrency / multithreding / race condition / a deadlock waiting to happen / c++ primitieves

- basics & questions

- memory allocation (deeper) - algs; system level

- cpp app segments; which what is stored; where what is created/removed

- insrastructure around - dynamic/static code checkers; profiling tools; unit/integration tests; continious integration

- STL

- templates

- MVP

- virtual process space

- process system features


#9) Finance things -

- read about entire trading stack, from market connectivity to core infra to trade logic to GUIs to post-trade analytics and tools.

- Unless your trade can be monolithic-per-server, you'll need to separate your long-lived components (market data, exchange connectivity, up 24/5) from short-lived components (trade, signals, sniffers, etc). 
That means running in their own processes, pinned to their own cores, NUMA-aware, communicating via IPC (shared memory queues, spin-locks, etc), minimizing thread context switches, etc...
This split also allows you to isolate network connectivity. 
Due to the slowness (for HFT) of kernel-based TCP/UDP processing, you have to use kernel bypass. 
For example, Solarflare cards with "openonload" have a hierarchy of kernel bypass APIs, each faster and lower-level than the other, but the differences can be dramatic, so you may have to code to the lowest-level.
The Market Data component deals with a huge amount of inbound market data - so you need fast (but tiny) decoders and tiny (but fast) lookups. 
Then you need smart (and compact) market book builder, event processing code, etc.
The Exchange component needs to be able to parse and build FIX very fast (using a bunch of tricks that everyone comes up with), but overall it's pretty straightforward (throttling, risk, order book management, etc)
The algo stack -- this can be broken up into multiple layers (risk, etc), and tends to have most variety of data structures. 
There's an Order (compact, typically broken up into hot and cold sections), an Order Book (many many ways to organize it), Stackers, Risk, Throttling, etc. 
All these DS's have to be checked for virtually any event, so there's huge d-cache pressure. 
This also tends to have the biggest variation in code, so there's i-cache pressure - different events cause different paths to be taken, etc.
So depending on where you are in the stack, you need to come up with typically non-standard data structures, and have to keep focus on the overall effect - this is different than many other jobs.
This is just for Futures (two main exchanges) -- I imagine it's similar but much worse for Equities (tons of venues) or Equity Options (tons of venues, tons of products)





