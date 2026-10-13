# Quantum ESPRESSO 7.6 — Reproducible Build Environment

## Reference hardware
- OS: CentOS Linux 8
- CPU: 2 x Intel Xeon Platinum 8180 @ 2.50 GHz
- Physical cores: 56
- Logical CPUs: 112
- NUMA nodes: 2

## Software versions
- QE source description: qe-7.6-1-g61569eb48
- Intel Fortran compiler: ifx 2026.1.1
- Intel MPI: 2021.18.1
- Intel oneMKL: 2026.1
- oneMKL version macro: INTEL_MKL_VERSION=20260100
- oneAPI root: /opt/intel/oneapi

## Compilers and parallel configuration
- MPI Fortran wrapper: mpiifx
- Fortran compiler: ifx
- C compiler: icx
- MPI enabled: yes
- OpenMP enabled: yes
- DFTI enabled: yes
- ScaLAPACK enabled: yes

## Compiler flags
- Optimization: -O3
- Architecture tuning: -xHost
- OpenMP: -qopenmp
- Fortran record length: -assume byterecl
- Debug/no-optimization flags: -O0 -assume byterecl -g -traceback

## Numerical libraries
- BLAS: -lmkl_intel_lp64 -lmkl_sequential -lmkl_core
- ScaLAPACK: -lmkl_scalapack_lp64
- BLACS: -lmkl_blacs_intelmpi_lp64
- Separate LAPACK library: not specified
- FFT library: QE internal configuration

## QE preprocessor definitions
- -D__DFTI
- -D__MPI
- -D__MPI_MODULE
- -D__SCALAPACK

## Reference configuration
The machine-specific configuration is saved in:
config/make.inc.xeon8180

The configuration uses absolute oneMKL include paths and must be
reviewed before use on another machine.

## Validation procedure
1. Build QE from the recorded source revision.
2. Use a compatible Intel compiler, MPI and numerical-library environment.
3. Run the same regression input on the target machine.
4. Verify successful completion, convergence and total energy.
5. Record MPI ranks, OpenMP threads and elapsed time.
6. Compare performance only under documented runtime settings.

## Portability notes
The -xHost flag targets the build machine's CPU.
Absolute paths, compiler versions, MPI compatibility and library
linking must be checked on each target system.

A successful build does not by itself establish numerical
reproducibility or equivalent performance.
