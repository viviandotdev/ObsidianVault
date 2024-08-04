---
created: <% tp.file.creation_date() %>
modified: <% tp.file.last_modified_date("dddd Do MMMM YYYY HH:mm:ss") %>
alias:
---
up::
tags:: #system-design
related:

## Check pointing

![[checkpointing.excalidraw|500]]

As events arrive, we store in the temporary storage (queue) and the processing service will **pull** these events from the storage sequentially.

Check pointing is a technique used to periodically save intermediate results of the data aggregation process. Checkpoints are created at predefined intervals.  **After a predefined number of events are processed and successfully stored in the database, we will create a checkpoint to write the intermediate data to some persistent storage.**

How do checkpoints ensure **consistency?**
1. By periodically saving intermediate results, all data is not lost when the processing service crashes. Instead of reprocessing all the values, we can load the check pointed data from the persistent storage. We only need to reprocess events that occurred after the last saved checkpoint.
2. Helps prevent data inconsistencies that can results from processing failures.

How do checkpoints ensure **fault tolerance?**
2. If failure occurs during aggregation process we can recover from the last saved checkpoint, avoids processing entire dataset from the beginning saving time and computational resources.
