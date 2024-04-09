# KNL-testing
Repository holding scripts and information regarding the testing done in South Africa to test the viabiliity of the KNL nodes.

---Compute node specs 
CPU op-mode(s):      32-bit, 64-bit
Byte Order:          Little Endian
CPU(s):              272
On-line CPU(s) list: 0-271
Thread(s) per core:  4
Core(s) per socket:  68
Socket(s):           1
NUMA node(s):        1
Vendor ID:           GenuineIntel
CPU family:          6
Model:               87
Model name:          Intel(R) Xeon Phi(TM) CPU 7250 @ 1.40GH
Stepping:            1
CPU MHz:             1600.000
CPU max MHz:         1600.0000
CPU min MHz:         1000.0000
BogoMIPS:            2793.58
L1d cache:           32K
L1i cache:           32K
L2 cache:            1024K
NUMA node0 CPU(s):   0-271
Flags:               fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush dts acpi mmx fxsr sse sse2 ss ht tm pbe syscall nx pdpe1gb rdtscp lm constant_tsc arch_perfmon pebs bts rep_good nopl xtopology nonstop_tsc cpuid aperfmperf pni pclmulqdq dtes64 monitor ds_cpl est tm2 ssse3 fma cx16 xtpr pdcm sse4_1 sse4_2 x2apic movbe popcnt tsc_deadline_timer aes xsave avx f16c rdrand lahf_lm abm 3dnowprefetch ring3mwait cpuid_fault epb pti fsgsbase tsc_adjust bmi1 avx2 smep bmi2 erms avx512f rdseed adx avx512pf avx512er avx512cd xsaveopt dtherm ida arat pln pts

 --How to get Compute node specs
 1. Initiate an a slurm interactive session
 srun --pty bash //Code to launch an interactive slurm session
 2. Run ff commands 
 lcpu
 lsmem


---HPL Benchmarks

### HPL dat file being used:

HPLinpack benchmark input file
Innovative Computing Laboratory, University of Tennessee
HPL.out      output file name (if any)
6            device out (6=stdout,7=stderr,file)
1            # of problems sizes (N)
50000         Ns
1            # of NBs
192           NBs
0            PMAP process mapping (0=Row-,1=Column-major)
1            # of process grids (P x Q)
17            Ps
32            Qs
16.0         threshold
1            # of panel fact
2            PFACTs (0=left, 1=Crout, 2=Right)
1            # of recursive stopping criterium
4            NBMINs (>= 1)
1            # of panels in recursion
2            NDIVs
1            # of recursive panel fact.
1            RFACTs (0=left, 1=Crout, 2=Right)
1            # of broadcast
1            BCASTs (0=1rg,1=1rM,2=2rg,3=2rM,4=Lng,5=LnM)
1            # of lookahead depth
1            DEPTHs (>=0)
2            SWAP (0=bin-exch,1=long,2=mix)
64           swapping threshold
0            L1 in (0=transposed,1=no-transposed) form
0            U  in (0=transposed,1=no-transposed) form
1            Equilibration (0=no,1=yes)
8            memory alignment in double (> 0)

##### This line (no. 32) is ignored (it serves as a separator). ######

0                               Number of additional problem sizes for PTRANS
1200 10000 30000                values of N
0                               number of additional blocking sizes for PTRANS
40 9 8 13 13 20 16 32 64        values of NB

Performance on no flags compile:
================================================================================
T/V                N    NB     P     Q               Time                 Gflops
--------------------------------------------------------------------------------
WR11C2R4       50000   192    17    32             509.41             1.6360e+02
HPL_pdgesv() start time Sat Apr  6 16:58:08 2024

HPL_pdgesv() end time   Sat Apr  6 17:06:37 2024

--VVV--VVV--VVV--VVV--VVV--VVV--VVV--VVV--VVV--VVV--VVV--VVV--VVV--VVV--VVV-
Max aggregated wall time rfact . . . :              16.16
+ Max aggregated wall time pfact . . :              15.90
+ Max aggregated wall time mxswp . . :              15.82
Max aggregated wall time update  . . :             502.19
+ Max aggregated wall time laswp . . :             391.45
Max aggregated wall time up tr sv  . :               0.34
--------------------------------------------------------------------------------
||Ax-b||_oo/(eps*(||A||_oo*||x||_oo+||b||_oo)*N)=   1.25554213e-03 ...... PASSED
================================================================================

Finished      1 tests with the following results:
              1 tests completed and passed residual checks,
              0 tests completed and failed residual checks,
              0 tests skipped because of illegal input values.
--------------------------------------------------------------------------------

End of Tests.

### Second Benchmark
================================================================================

================================================================================
T/V                N    NB     P     Q               Time                 Gflops
--------------------------------------------------------------------------------
WR11C2R4       50000   192    17    32             502.94             1.6570e+02
HPL_pdgesv() start time Sat Apr  6 17:33:31 2024

HPL_pdgesv() end time   Sat Apr  6 17:41:54 2024

--VVV--VVV--VVV--VVV--VVV--VVV--VVV--VVV--VVV--VVV--VVV--VVV--VVV--VVV--VVV-
Max aggregated wall time rfact . . . :              13.79
+ Max aggregated wall time pfact . . :              13.52
+ Max aggregated wall time mxswp . . :              13.44
Max aggregated wall time update  . . :             495.13
+ Max aggregated wall time laswp . . :             383.85
Max aggregated wall time up tr sv  . :               0.34
--------------------------------------------------------------------------------
Ax-b_oo/(eps(A_oox_oo+b_oo)*N)=   1.25554213e-03 ...... PASSED
================================================================================

Finished      1 tests with the following results:
              1 tests completed and passed residual checks,
              0 tests completed and failed residual checks,
              0 tests skipped because of illegal input values.
--------------------------------------------------------------------------------

End of Tests.
================================================================================

With flags : -mavx512f -mavx512cd -mavx512er -mavx512pf -falign-functions=64 -falign-loops=64


