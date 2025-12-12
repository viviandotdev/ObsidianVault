**Threads**
what are threads?
- they are a stack of instructions that can run at the same time in an program.
- threads have shared memory, meaning that if you have a array and all the threads in that program have access to that same array

how are threads used in the context of distributed systems?
- a thread might be used to create a remote procedure call to thousands of different servers
	- the when the RPC is complete the thread will continue?

what are the challenges/problems of coding threads
**[[Race condition]]**
	suppose we have a function to 
	n = n + 1
	thread one starts this function
	**however thread two also enters this function before thread one has completed**
	as a result thread one and thread two will both increment by n = 1
	rather than n = 2

how can we solve this race condition?
using mu **[[locks]]**
```
mu lock
n = n + 1
mu unlock
```
in a go program you can put a lock around a function, this tells the second thread that it must wait for this block to be unlocked before it can run the block of code.

what does it be for thread instructions to be atomic?


what are RPC (remote procudure calls in Go?)

**web crawler as an example**
what is web crawler?

what some challenges when creating a web crawler?
- fetch twice
- cycles
- fetch many pages in parallell
- what is the call finished?
**serial cralwer**
- dfs
-  