## NYU HPC HW4.
### Mu-Hua Chien 
### mhc431@nyu.edu

mpi_bug1: 

1. For the rank 2, the recv before the send function, so the rank cannot send the information before it receive. Hence it hangs.   

2. The pair of send and recv function do not have the same tag, so the cannot receive the information.   


mpi_bug2:
 
The alpha and beta does not share the same data type, so the datatype in mpi_irecv, MPI_float, is modified. 

mpi_bug3: 

This file does not include mpi_initial and mpi_finalize. 

mpi_bug4: 

The master rank does not see the mpi_reduce. Add the end line before the master rank print the answer. 

mpi_bug5: 

For openmpi, the first 10000 number of communication is done in O(0.0010) sec but for rest of communication, it takes times to finish, because most of communication does not finish with the receive node. Hence the communication speed is reduced. 

For mvapich2, the communication stacks the internet at the beginning, so it cannot reach speed as fast as we obtain in the beginning of openmpi.

Therefore, we should maintain same amount of computation for each node, so that we can have efficient communication.  

mpi_bug6: 

The bugs appear in mpi_waitall since the input considers all the local variables. 

For rank 0 and 1, there are 2xRESP requests, starting from 0 - 2xRESP, so both ranks have nreqs = 2xRESP and should start with 0 , not RESP in rank 1.

For rank 2, there is no request, so the nreqs = 0.

For rank 3, there are RESP requests, so there is no need to change. 

 
