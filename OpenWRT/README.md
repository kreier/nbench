# Version for OpenWRT

The benchmark can be easily crosscompiled, you just have to change the compiler to `mips-openwrt-linux-musl-gcc`. But the 5th benchmark, **ASSIGNMENT**, will be stuck in a forever loop. Here is the workaround and patched edition:

## Workaround

The assignment test is now automatically disabled on MIPS builds to prevent hanging. The code checks for `__mips__` or `_MIPS_ISA_MIPS` defines and skips the assignment test.

## Compile on OpenWRT with the SDK and toolchain

First download the toolchain from [downloads.openwrt.org/releases/25.12.2/targets/ath79/generic/](https://downloads.openwrt.org/releases/25.12.2/targets/ath79/generic/) (at the very bottom):

``` sh
apt install build-essential libncurses-dev zlib1g-dev gawk git gettext libssl-dev xsltproc rsync wget unzip python3 zstd
wget https://downloads.openwrt.org/releases/25.12.2/targets/ath79/generic/openwrt-sdk-25.12.2-ath79-generic_gcc-14.3.0_musl.Linux-x86_64.tar.zst
tar xvf openwrt-sdk-25.12.2-ath79-generic_gcc-14.3.0_musl.Linux-x86_64.tar.zst
make defconfig
make toolchain/install
export PATH=~/github/openwrt-sdk-25.12.2-ath79-generic_gcc-14.3.0_musl.Linux-x86_64/staging_dir/toolchain-mips_24kc_gcc-14.3.0_musl/bin:$PATH
export STAGING_DIR=~/github/openwrt-sdk-25.12.2-ath79-generic_gcc-14.3.0_musl.Linux-x86_64/staging_dir
```

Then get nbench

``` sh
wget kreier.org/docs/nbench.tar.gz
tar xf nbench.tar.gz
cd nbench-byte-2.2.3
make
```

## Example verbose output

With the `-v` flag you can get a verbose output for each of the 10 benchmarks. We added the elapsed time in each benchmark with the help of Codex. The result:

``` sh
mk@i7-13700T:~/github/benchmark/nbench$ ./nbench -v

BYTEmark* Native Mode Benchmark ver. 2 (10/95)
Index-split by Andrew D. Balsa (11/97)
Linux/Unix* port by Uwe F. Mayer (12/96,11/97)

============================== ALL STATISTICS ===============================
**Date and time of benchmark run: Sun Apr  5 06:52:17 2026
**Sizeof: char:1 short:2 int:4 long:8 u8:1 u16:2 u32:4 int32:4
**System used for compilation:
**Linux i7-13700T 6.6.75.1-microsoft-standard-WSL2 #1 SMP PREEMPT_DYNAMIC Sat Fe
**C compiler: gcc version 13.3.0 (Ubuntu 13.3.0-6ubuntu2~24.04.1)
**libc: /lib/x86_64-linux-gnu/libc.so.6
**Date of compilation: Sun Apr  5 06:52:11 +07 2026
=============================================================================

TEST                : Iterations/sec.  : Old Index   : New Index
                    :                  : Pentium 90* : AMD K6/233*
--------------------:------------------:-------------:------------

[DEBUG] Starting test 0: NUMERIC SORT
NUMERIC SORT        :  [DEBUG] Run 1 of 5+ (fid=0)...
  [DEBUG] Run 1 completed, score=2566.02
  [DEBUG] Run 2 of 5+ (fid=0)...
  [DEBUG] Run 2 completed, score=2536.11
  [DEBUG] Run 3 of 5+ (fid=0)...
  [DEBUG] Run 3 completed, score=2532.93
  [DEBUG] Run 4 of 5+ (fid=0)...
  [DEBUG] Run 4 completed, score=2525.48
  [DEBUG] Run 5 of 5+ (fid=0)...
  [DEBUG] Run 5 completed, score=2510.55
          2534.2  :      64.99  :      21.34
  Elapsed time: 27.294 sec
  Absolute standard deviation: 20.3288
  Relative standard deviation: 0.802174 %
  Number of runs: 5
  Number of arrays: 1
  Array size: 8111
Done with NUMERIC SORT


[DEBUG] Starting test 1: STRING SORT
STRING SORT         :  [DEBUG] Run 1 of 5+ (fid=1)...
  [DEBUG] Run 1 completed, score=3494
  [DEBUG] Run 2 of 5+ (fid=1)...
  [DEBUG] Run 2 completed, score=3295.75
  [DEBUG] Run 3 of 5+ (fid=1)...
  [DEBUG] Run 3 completed, score=3154.65
  [DEBUG] Run 4 of 5+ (fid=1)...
  [DEBUG] Run 4 completed, score=3374.59
  [DEBUG] Run 5 of 5+ (fid=1)...
  [DEBUG] Run 5 completed, score=3382.9
          3340.4  :    1492.57  :     231.02
  Elapsed time: 28.716 sec
  Absolute standard deviation: 125.56
  Relative standard deviation: 3.75887 %
  Number of runs: 5
  Number of arrays: 1
  Array size: 8111
Done with STRING SORT


[DEBUG] Starting test 2: BITFIELD
BITFIELD            :  [DEBUG] Run 1 of 5+ (fid=2)...
  [DEBUG] Run 1 completed, score=1.17517e+09
  [DEBUG] Run 2 of 5+ (fid=2)...
  [DEBUG] Run 2 completed, score=1.16526e+09
  [DEBUG] Run 3 of 5+ (fid=2)...
  [DEBUG] Run 3 completed, score=1.15943e+09
  [DEBUG] Run 4 of 5+ (fid=2)...
  [DEBUG] Run 4 completed, score=1.19128e+09
  [DEBUG] Run 5 of 5+ (fid=2)...
  [DEBUG] Run 5 completed, score=1.15571e+09
      1.1694e+09  :     200.59  :      41.90
  Elapsed time: 25.064 sec
  Absolute standard deviation: 1.42813e+07
  Relative standard deviation: 1.22128 %
  Number of runs: 5
  Operations array size: 30
  Bitfield array size: 16384
Done with BITFIELD


[DEBUG] Starting test 3: FP EMULATION
FP EMULATION        :  [DEBUG] Run 1 of 5+ (fid=3)...
  [DEBUG] Run 1 completed, score=1230.14
  [DEBUG] Run 2 of 5+ (fid=3)...
  [DEBUG] Run 2 completed, score=1292.55
  [DEBUG] Run 3 of 5+ (fid=3)...
  [DEBUG] Run 3 completed, score=1326.43
  [DEBUG] Run 4 of 5+ (fid=3)...
  [DEBUG] Run 4 completed, score=1302.63
  [DEBUG] Run 5 of 5+ (fid=3)...
  [DEBUG] Run 5 completed, score=1329.65
          1296.3  :     622.01  :     143.53
  Elapsed time: 25.033 sec
  Absolute standard deviation: 40.161
  Relative standard deviation: 3.09817 %
  Number of runs: 5
  Number of loops: 1
  Array size: 3000
Done with FP EMULATION


[DEBUG] Starting test 4: FOURIER
FOURIER             :  [DEBUG] Run 1 of 5+ (fid=4)...
  [DEBUG] Run 1 completed, score=317402
  [DEBUG] Run 2 of 5+ (fid=4)...
  [DEBUG] Run 2 completed, score=320714
  [DEBUG] Run 3 of 5+ (fid=4)...
  [DEBUG] Run 3 completed, score=324266
  [DEBUG] Run 4 of 5+ (fid=4)...
  [DEBUG] Run 4 completed, score=322244
  [DEBUG] Run 5 of 5+ (fid=4)...
  [DEBUG] Run 5 completed, score=321745
      3.2127e+05  :     365.38  :     205.22
  Elapsed time: 25.013 sec
  Absolute standard deviation: 2521.08
  Relative standard deviation: 0.784713 %
  Number of runs: 5
  Number of coefficients: 100
Done with FOURIER


[DEBUG] Starting test 5: ASSIGNMENT
ASSIGNMENT          :  [DEBUG] Run 1 of 5+ (fid=5)...
  [DEBUG] Run 1 completed, score=100.763
  [DEBUG] Run 2 of 5+ (fid=5)...
  [DEBUG] Run 2 completed, score=104.076
  [DEBUG] Run 3 of 5+ (fid=5)...
  [DEBUG] Run 3 completed, score=99.2979
  [DEBUG] Run 4 of 5+ (fid=5)...
  [DEBUG] Run 4 completed, score=103.915
  [DEBUG] Run 5 of 5+ (fid=5)...
  [DEBUG] Run 5 completed, score=106.762
          102.96  :     391.79  :     101.62
  Elapsed time: 25.173 sec
  Absolute standard deviation: 2.95182
  Relative standard deviation: 2.86688 %
  Number of runs: 5
  Number of arrays: 1
Done with ASSIGNMENT


[DEBUG] Starting test 6: IDEA
IDEA                :  [DEBUG] Run 1 of 5+ (fid=6)...
  [DEBUG] Run 1 completed, score=23158.4
  [DEBUG] Run 2 of 5+ (fid=6)...
  [DEBUG] Run 2 completed, score=24996.9
  [DEBUG] Run 3 of 5+ (fid=6)...
  [DEBUG] Run 3 completed, score=24897.5
  [DEBUG] Run 4 of 5+ (fid=6)...
  [DEBUG] Run 4 completed, score=25308.3
  [DEBUG] Run 5 of 5+ (fid=6)...
  [DEBUG] Run 5 completed, score=25536
           24779  :     378.99  :     112.53
  Elapsed time: 25.012 sec
  Absolute standard deviation: 940.905
  Relative standard deviation: 3.79712 %
  Number of runs: 5
  Array size: 4000
 Number of loops: 100
Done with IDEA


[DEBUG] Starting test 7: HUFFMAN
HUFFMAN             :  [DEBUG] Run 1 of 5+ (fid=7)...
  [DEBUG] Run 1 completed, score=14310.2
  [DEBUG] Run 2 of 5+ (fid=7)...
  [DEBUG] Run 2 completed, score=13568.7
  [DEBUG] Run 3 of 5+ (fid=7)...
  [DEBUG] Run 3 completed, score=13527.9
  [DEBUG] Run 4 of 5+ (fid=7)...
  [DEBUG] Run 4 completed, score=13361.4
  [DEBUG] Run 5 of 5+ (fid=7)...
  [DEBUG] Run 5 completed, score=13816.3
           13717  :     380.37  :     121.46
  Elapsed time: 25.030 sec
  Absolute standard deviation: 369.469
  Relative standard deviation: 2.69353 %
  Number of runs: 5
  Array size: 5000
  Number of loops: 100
Done with HUFFMAN


[DEBUG] Starting test 8: NEURAL NET
NEURAL NET          :  [DEBUG] Run 1 of 5+ (fid=8)...
  [DEBUG] Run 1 completed, score=324.918
  [DEBUG] Run 2 of 5+ (fid=8)...
  [DEBUG] Run 2 completed, score=338.567
  [DEBUG] Run 3 of 5+ (fid=8)...
  [DEBUG] Run 3 completed, score=320.412
  [DEBUG] Run 4 of 5+ (fid=8)...
  [DEBUG] Run 4 completed, score=234.469
  [DEBUG] Run 5 of 5+ (fid=8)...
  [DEBUG] Run 5 completed, score=259.291
  [DEBUG] Additional run, attempt 6 of 30 (fid=8)...
  [DEBUG] Run 6 completed, score=329.42
  [DEBUG] Additional run, attempt 7 of 30 (fid=8)...
  [DEBUG] Run 7 completed, score=335.437
  [DEBUG] Additional run, attempt 8 of 30 (fid=8)...
  [DEBUG] Run 8 completed, score=307.944
  [DEBUG] Additional run, attempt 9 of 30 (fid=8)...
  [DEBUG] Run 9 completed, score=302.255
  [DEBUG] Additional run, attempt 10 of 30 (fid=8)...
  [DEBUG] Run 10 completed, score=321.744
  [DEBUG] Additional run, attempt 11 of 30 (fid=8)...
  [DEBUG] Run 11 completed, score=330.53
  [DEBUG] Additional run, attempt 12 of 30 (fid=8)...
  [DEBUG] Run 12 completed, score=329.596
  [DEBUG] Additional run, attempt 13 of 30 (fid=8)...
  [DEBUG] Run 13 completed, score=335.615
  [DEBUG] Additional run, attempt 14 of 30 (fid=8)...
  [DEBUG] Run 14 completed, score=331.738
  [DEBUG] Additional run, attempt 15 of 30 (fid=8)...
  [DEBUG] Run 15 completed, score=331.646
  [DEBUG] Additional run, attempt 16 of 30 (fid=8)...
  [DEBUG] Run 16 completed, score=334.053
          316.73  :     508.80  :     214.02
  Elapsed time: 80.044 sec
  Absolute standard deviation: 29.3335
  Relative standard deviation: 9.26146 %
  Number of runs: 16
  Number of loops: 1
Done with NEURAL NET


[DEBUG] Starting test 9: LU DECOMPOSITION
LU DECOMPOSITION    :  [DEBUG] Run 1 of 5+ (fid=9)...
  [DEBUG] Run 1 completed, score=8848.33
  [DEBUG] Run 2 of 5+ (fid=9)...
  [DEBUG] Run 2 completed, score=8558.17
  [DEBUG] Run 3 of 5+ (fid=9)...
  [DEBUG] Run 3 completed, score=8524.08
  [DEBUG] Run 4 of 5+ (fid=9)...
  [DEBUG] Run 4 completed, score=8663.1
  [DEBUG] Run 5 of 5+ (fid=9)...
  [DEBUG] Run 5 completed, score=8695.76
          8657.9  :     448.52  :     323.88
  Elapsed time: 25.455 sec
  Absolute standard deviation: 128.04
  Relative standard deviation: 1.47888 %
  Number of runs: 5
  Number of arrays: 1
Done with LU DECOMPOSITION

Benchmark step timing summary:
   1. NUMERIC SORT     : 27.294 sec
   2. STRING SORT      : 28.716 sec
   3. BITFIELD         : 25.064 sec
   4. FP EMULATION     : 25.033 sec
   5. FOURIER          : 25.013 sec
   6. ASSIGNMENT       : 25.173 sec
   7. IDEA             : 25.012 sec
   8. HUFFMAN          : 25.030 sec
   9. NEURAL NET       : 80.044 sec
  10. LU DECOMPOSITION : 25.455 sec

==========================ORIGINAL BYTEMARK RESULTS==========================
INTEGER INDEX       : 353.041
FLOATING-POINT INDEX: 436.851
Baseline (MSDOS*)   : Pentium* 90, 256 KB L2-cache, Watcom* compiler 10.0
==============================LINUX DATA BELOW===============================
CPU                 : 24 CPU GenuineIntel 13th Gen Intel(R) Core(TM) i7-13700T 1382MHz
L2 Cache            : 30720 KB
OS                  : Linux 6.6.75.1-microsoft-standard-WSL2
C compiler          : gcc version 13.3.0 (Ubuntu 13.3.0-6ubuntu2~24.04.1)
libc                : /lib/x86_64-linux-gnu/libc.so.6
MEMORY INDEX        : 99.452
INTEGER INDEX       : 80.442
FLOATING-POINT INDEX: 242.299
Baseline (LINUX)    : AMD K6/233*, 512 KB L2-cache, gcc 2.7.2.3, libc-5.4.38
* Trademarks are property of their respective holder.
```
