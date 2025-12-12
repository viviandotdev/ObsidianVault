**Threads**
==what are threads?==
- they are a stack of instructions that can run at the same time in an program.
- threads have shared datadddd, meaning that if you have a array and all the threads in that program have access to that same array

==how are threads used in the context of distributed systems?==
- a thread might be used to create a remote procedure call to thousands of different servers
	- the when the RPC is complete the thread will continue?

==what are the challenges/problems of coding threads==
**[[Race condition]]**
	suppose we have a function to 
	n = n + 1
	thread one starts this function
	**however thread two also enters this function before thread one has completed**
	as a result thread one and thread two will both increment by n = 1
	rather than n = 2

==how can we solve this race condition?==
using mu **[[locks]]**
```
mu lock
n = n + 1
mu unlock
```
in a go program you can put a lock around a function, this tells the second thread that it must wait for this block to be unlocked before it can run the block of code.

==what does it mean for thread instructions to be atomic?==


==what are RPC (remote procedure calls in Go?)==


==why is go the preferred language of use?==

**[[Design A Web Crawler|Web Crawler]] as an example**
==what is web crawler?==
purpose is to -> download the related contents of the web
1. start with a set of webpages
2. extract the urls on that web page 
3. download the urls then, repeat these steps recursively starting from theses new urls.
==what some challenges when creating a web crawler?==
- fetch twice, 
- how do we prevent **cycles**, where it visiting sites already visited
- we need to fetch many pages in parallel, or else it would just take forever
- when is the call finished?, this is recursive, how do we know what is it done
**the algorithm for a serial web crawler**
```go
func Serial(url string, fetcher Fetcher, fetched map[string]bool) {
	// Check if the URL has already been fetched.
	if fetched[url] {
		return
	}

	// Mark the URL as fetched before processing to avoid infinite loops in cycles.
	fetched[url] = true

	// Fetch the URLs linked from the current URL.
	urls, err := fetcher.Fetch(url)
	if err != nil {
		return // Stop processing this branch on error
	}
	// Recursively call Serial for each sub-URL found.
	for _, u := range urls {
		Serial(u, fetcher, fetched)
	}
	
	return
}
```

**serial cralwer**
- Uses [[Depth First Search]] !create dfs page
- no concurrecny, 
- 
-  