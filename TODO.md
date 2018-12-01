# topics to revise / learn

void* dynamic cast
order of initialisation
memory allocation algorithms
c++ app segments; where what is stored
multithreding


This is just a generic answer, I know:
Unless your trade can be monolithic-per-server, you'll need to separate your long-lived components (market data, exchange connectivity, up 24/5) from short-lived components (trade, signals, sniffers, etc). That means running in their own processes, pinned to their own cores, NUMA-aware, communicating via IPC (shared memory queues, spin-locks, etc), minimizing thread context switches, etc...
This split also allows you to isolate network connectivity. Due to the slowness (for HFT) of kernel-based TCP/UDP processing, you have to use kernel bypass. For example, Solarflare cards with "openonload" have a hierarchy of kernel bypass APIs, each faster and lower-level than the other, but the differences can be dramatic, so you may have to code to the lowest-level.
The Market Data component deals with a huge amount of inbound market data - so you need fast (but tiny) decoders and tiny (but fast) lookups. Then you need smart (and compact) market book builder, event processing code, etc.
The Exchange component needs to be able to parse and build FIX very fast (using a bunch of tricks that everyone comes up with), but overall it's pretty straightforward (throttling, risk, order book management, etc)
The algo stack -- this can be broken up into multiple layers (risk, etc), and tends to have most variety of data structures. There's an Order (compact, typically broken up into hot and cold sections), an Order Book (many many ways to organize it), Stackers, Risk, Throttling, etc. All these DS's have to be checked for virtually any event, so there's huge d-cache pressure. This also tends to have the biggest variation in code, so there's i-cache pressure - different events cause different paths to be taken, etc.
So depending on where you are in the stack, you need to come up with typically non-standard data structures, and have to keep focus on the overall effect - this is different than many other jobs.
This is just for Futures (two main exchanges) -- I imagine it's similar but much worse for Equities (tons of venues) or Equity Options (tons of venues, tons of products)

entire trading stack, from market connectivity to core infra to trade logic to GUIs to post-trade analytics and tools.

race condition, a deadlock waiting to happen, or a potential buffer overflow


https://www.geeksforgeeks.org/c-plus-plus/


https://encelo.github.io/notes.html

effective modern c++ vs professional c++