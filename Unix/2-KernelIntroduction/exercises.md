# Exercises

1. While the ampersand asks the shell to run the command in the background, no
   such inquiry is made with the pipe. The pipe is simply another stage in the
   sequence of provided commands; the command to the left of the pipe must fully
   execute before its output is to be provided to the command to the right of
   the pipe.
   
2. In the case where _bp_ is removed from the linked list, the linked list
   remains consistent. 
   
   In the case where _bp1_ is removed, the list is inconsistent. _bp1_ remains
   accessible via `bp1->forp->backp`, and _bp_ is no longer accessible going
   backward since `bp1->backp` has been removed.
   
   In the case where the structure that follows _bp1_, let's call it _bp2_, is
   removed, the effect is that both _bp2_ and _bp1_ are removed from the list.
   
3. Nothing out of the ordinary would occur because the kernel is not concerned
   with actively awakening processes; it is the responsibility of the processes
   to check their wake up condition and awaken themselves if the condition is
   satisfied. The kernel is simply going about its business as normal.
