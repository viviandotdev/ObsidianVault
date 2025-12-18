**always start with questions**
**questions you find the most interesting**
**engage with content while looking for answers to those questions**

**what is google file system**?
it is a distributed system that allows google to





What is strong consistency 
Emulates single server system

What are the trade offs of strong consistency?
Performance because extra communication is needed to be consistent slowing down and complicating the system

Problems with replicationq

Components of gfs
Master
And chunk servers

What data is stored in master?
Filename maps to array of chunk handles


Which data is in disk or ram

How is the log or check point stored in the master? A log is details of the action?
What is the checkpoint like where you can back up from?
What are the steps of a read?
Send file name and offset
Master knows which chunk server this data is found and then the list of chunk servers
The client talks to the correct chunk server that master told it to look at and gets the data

What does it mean for a chunk handle to be primary???
A chunk is data in a file and we need to know which chunk servers from the list of replicated chunk servers in the handle is the primary one all the others are secondary

Chunk handle represents some data in the file and which which servers does this data belong to

Read
How down it knownwhich chunk servers to look at?


What are the writes?