# The Buffer Cache

* buffer cache is pool of frequently used data blocks; minimize disk access for
  sake of time
  
## Buffer Headers

* buffer consists of memory array that contains data and buffer header that
  identifies buffer
* disk block cannot map to more than one buffer at a time

## Structure of the Buffer Pool

* kernel returns buffers to tail of free list
* kernel can grab specific buffers from anywhere in the list, should it need to
  grab the data assigned to a particular buffer
  - this task done with assistance of hash queue, so that the free list does not
    have to be directly searched
* therefore, frequently used buffers are located further from head
* kernel grabs buffer from free list when it needs _any_ free buffer

## Scenarios for Retrieval of a Buffer

* when writing to disk block, kernel checks if buffer for block exists
  - if yes, grab the buffer
  - if no, allocate a free buffer
* all buffers always located in a hash queue
  - selectively removed from free list as buffer is used, but position in hash
    queue does not change
* when process finishes using buffer, placed back on tail of free list, but
  contents retained
* buffers whose contents need to be written to disk before they can be
  repurposed are placed at head of free list to indicate that they had not been
  recently utilized (as proven by the need to free up the buffer) 
* the kernel can guarantee the processes sleeping for a buffer eventually wake up

## Reading and Writing Disk Blocks

* for asynchronous write, kernel starts I/O operation immediately, but does not
  wait for completion; does not have special "wait until last minute" privileges
  of delayed write
  
## Advantages and Disadvantages of the Buffer Cache

* kernel does not need to know anything about data being accessed; just copies
  whatever into buffer
* no special, potentially hardware dependent, data alignment is needed; kernel
  aligns data internally
* reduces the number of disk writes: frequently accessed data stays in memory,
  only being written to disks if not accessed in a while
* number of buffers must be carefully configured according to available system
  memory
* help ensure file system integrity by disallowing simultaneous buffer (data) access
* holding data in memory increases vulnerability to crashes; frequent flushing
  is recommended to combat problem; issue remains where user never knows exactly
  when data is written to disk
* extra copy of data is required when reading and writing to and from user
  processes; slows down performance when copying large amounts of data; improves
  performance for small data because writing to disk is only done at economical times
