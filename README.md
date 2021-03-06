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

mpi_bug7: 

For the mpi_bcast, the counts does not agree to all the rank, so its hangs because some ranks expect more data form rank 0, but it does not. 

jacobi-mpi2D:

Initial error = 8.00e+03

TACC: Setting up parallel environment for MVAPICH2+mpispawn.

non-blocking 

ibrun ./jacobi-mpi2D 1000 1000

non-blocking
Numer of iteration 1000, residual = 7.950528e+03, Time elapsed is 7.469062 secs.

ibrun ./jacobi-mpi2D-blocking 1000 1000

blocking
Numer of iteration 1000, residual = 7.950528e+03, Time elapsed is 7.564017 secs.

Strong scaling test on Stampede

Set total N = 4096 fixed. (Unit second)

|N procs(N per node) | 1(4096) | 4(2048) | 16(1024) | 64(512) | 256(256) | 
|---|---|---|---|---|---|
|non-blocking| 63.7981 | 19.3214 | 7.6027 | 1.9186| 0.4271|
|blocking| 63.8024 | 19.3377| 7.5161 | 1.8861 | 0.4271 | 

Weak scaling test on Stampede.

Set N per node = 256 fixed. (Unit second)

|N procs(total N) | 1(256) | 4(512) | 16(1024) | 64(2048) | 256(4096) |
|---|---|---|---|---|---|
|non-blocking| 0.3191 | 0.2984 | 0.3366 | 0.3372 | 0.3947 |
|blocking| 0.3187 | 0.3012 | 0.3396 | 0.3387 | 0.4196 | 

ssort: 

Sample sort test for differrnt N on each node with 64 cores.

| N /core  | 1E3 | 1E4 | 1E5 | 1E6 | 1E7 |
|---|---|---|---|---|---|
|time | 0.023300 | 0.010456 | 0.106580 | 1.246840 | 14.287363 |

