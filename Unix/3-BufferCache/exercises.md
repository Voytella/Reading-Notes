# Exercises

1. 

2. The case may arise that, immediately after checking the free list and
   identifying the buffer to be removed, the executing _getblk_ process is
   interrupted by a separate _getblk_ process that performs the same check,
   identifies the same buffer, and proceeds to remove it. When the initial
   _getblk_ is resumed, it will attempt to remove a buffer that no longer
   exists, and the system will be left in an inconsistent state. Therefore,
   the processor priority level must be elevated before the free list is checked.

3. Interrupts must be blocked before making a busy check for the same reasons
   mentioned in Question 2. If a competing _getblk_ process interrupts the
   executing _getblk_ process immediately after the executing _getblk_ process
   identified the busy status of a block, the competing _getblk_ process can
   change the busy status of the block, thus leaving thy system in an
   inconsistent state.

4. No, buffers with invalid contents should not appear on a hash queue. When the
   kernel requests _any_ buffer, it takes the buffer at the head of the free
   list and overwrites it with the newly requested data. Buffers on a hash queue
   may be readily accessed regardless of their position in the free
   list. _brelse_ places buffers with invalid contents at the head of the free
   list in order to ensure that the buffer's memory is filled with usable, valid
   data as quickly as possible. If that buffer is located in a hash queue,
   however, its ID could be requested, and the invalid contents served up to a
   process before it is overwritten. In order to prevent a process from
   potentially receiving invalid data, buffers whose contents are invalid must
   not appear on a hash queue.
