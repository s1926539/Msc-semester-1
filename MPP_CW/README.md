﻿#**Instructions for using percolate parallel code decomposed by two-dimensional domain**

------

The file describes the file distribution of the code, the implementation functions of each source file, the operation instructions, the operation code examples and precaution.It is divided into the following modules:

> * Code structure
> * Function package description
> * Operation demonstration
> * Operation precautions


## **Code structure**

### File distribution

The source files of the whole code are stored in the folder names src. The header file of the code is stored in the sub folder of src named src_h. There are 6 source files in src folder, which are uni.c,percwritedynamic.c,percolate.c,parallelpart.c,ChangeGridValue.c and arralloc.c.It has four head files which are percolate.h, parallel.h, Changevalue.h and arralloc.h.

### **Function encapsulation**  
#### **percwritedynamic.c**  
The functions in the header file are the functions provided by the course. It can generate a PGM file for the pointer map generated by percolate.

#### **ChangeGridValue.c**  
Three nine functions are encapsulated in this file. The random_filledsquare function is used to randomly initialize the map value. The SetOriginialvalue function initializes the smallmap pointer with a halo. The UpdateSmallmapvalue function assigns the value in the updated smallmap pointer old to smallmap，which updates the smallmap value after communication.

The isLastRow function is used to determine whether the process is in the last row of Cartesian topology when the process level is i. isLastCol determines whether it is in the last column. The typeIdx function determines the type of data sent by each process. Rowcol function is used to determine the coordinates of each process in Cartesian coordinate system on the main process according to the level of each process. The smallmap0 and smallmap1 functions determine the M and N values of the smallmap at rank i.
#### **parallelpart.c**  
There are three functions in this file. These three functions implement the initialization of the parameter values of the MPI_Alltoalw function, the initialization of the parameter values of the MPI_Alltoalw function in the main process rank 0, and the parallel update of the smallmap of each process, with communication with each other.
## **Function package description** 
The build command of the code is implemented through the makefile function.But it must be built with the MPT  and Intel compilers-18 modules loaded. So users just need to type make directly on the command line to compile the entire code after loading MPT  and Intel compilers-18 modules.
The specific commands are as follows:

module load mpt
module load intel-compilers-18
make
## **Operation demonstration**
### **Front-end operation** 
After compiling through Makefile, enter the command:

mpirun - n [P] ./percolate [seed]

Where P is the number of processors running in parallel, seed is the random number of percolate, and the size range is [0,900 000 000]. Take the original case as an example. If users want to run the function with random number on 15 processes, just enter:

mpirun - n 15 ./percolate 1564

Note: when changing the value of the number of processors, please modify the P value defined in the percolate.h header file in the src_h folder as the same size of the number of processors. Otherwise, the program will output that the P value is different from the number of processes and exit.
If users want to change the edge length L of the grid, they only need to modify the defined L value in the percolate.h.
### **Back-end operation** 
Users just need to change the value of 'NPROC' variable to the number of processors P in 'percolate.pbs' file. When the number of processors P is greater than 36, please adjust the value of a in select=[a]:ncpus=36 so that a can divide P by integer.
The P value needs to be the same as the P value defined in percolate.h.
## **Operation precautions**
The program can deal with parallel percolate code decomposed by two-dimensional domain in all cases. However, it should be noted that when  running the code, the number of processors should be the same as the P value in percolate.h.

------

 

