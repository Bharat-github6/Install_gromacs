# Install_gromacs
## Install GROMACS and all the other dependecy
GROMACS has been a most used Molecular dynamics simulation engine in the last couple of years. Thanks to the  increasing power of computer. When I staret doing simnulation 
GROMACS was installe on our computing cluster and I had started right way to do the simulation. Later  when I need to used some recent version of it, I was perplexed. I have included 
here how to install GROMACS so we can make most of it and patch GROMACS with PLUMED. PLUMED is a PLUmed MolEcular Dynamics simulation package which is very useful in estimating free energy. 
It has both Umbrella Sampling and Metadynamics techniques. All this installation tutorial is  intended for HPC but it also works for a personal machine too

 ### Depencency (latest version will be better)


  - gcc compiler 
  - fftw 
  - OpenMPI (for parallelization)
  - cmake


### Start with compiling gcc

I prefer to download all the software and compiler in the source folder.
Download the gcc compiler directly to your machine

```python
wget http://mirror.rit.edu/gnu/gcc/gcc-8.5.0/gcc-8.5.0.tar.gz
```

Extract the files

``` bash
tar -xvf gcc-8.5.0/gcc-8.5.0.tar.gz
```

Go to gcc-8.5.0 folder

```python

cd gcc-8.5.0

```
Download all the prerequisite for gcc to compile

```python

 sh contrib/download_prerequisites
 
 ```
 

make a new directory inside gcc-8.5.0 and go to that folder

```python

mkdir build
cd build

```

Configure

```python

../configure --prefix=/lscratch/apps/gcc/8.5.0 --enable-languages=c,c++,fortran,go --disable-multilib

```
Compile (this will take a little while ~20 mins

```python
make- j 10 bootstrap

```

Install

```
make install

```

CONGRATULATIONS!!! gcc is now installed


If you are working in a HPC it is always helpful to make a modulefiles for all the software that you installed. Lets make a module file for gcc. Make a folder called modulesfiles in your home directory and make a gcc folder inside modulefiles

```python
mkdir modulefiles
cd modulefiles
mkdir gcc
```
Make module files with in it. I named this module file according to version of the software because it will be easier if I have to installed the updated one again. 
```
touch 8.5.0
```

paste this lines to the 8.5.0 file

```
#%Module1.0 
set root_dir /lscratch/apps/gcc/8.5.0 
prepend-path LD_LIBRARY_PATH $root_dir/lib:$root_dir/lib64 
prepend-path MANPATH $root_dir/share/man 
prepend-path PATH $root_dir/bin 
prepend-path CMAKE_PREFIX_PATH $root_dir 
setenv CC   gcc 
setenv CXX  g++ 
setenv FC   gfortran 
setenv F77  gfortran 
setenv F90  gfortran 
setenv F95  gfortran
```




 

NOTE: To specify a default module within a modulefiles folder (In case if you have multiple version) , create a file called .version and paste the lines below
 
 ```python
#%Module1.0# 
set ModulesVersion  "gcc-8.5.0" 
```
 

Now you can import the gcc compiler in you machine

```python
module load gcc-8.5.0
```

Now install FFTW, will come back later and complete it.

