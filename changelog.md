# Changelog

## v1.2 Source for DOS, adaptation for Linux - 1996/12/16

- The source for DOS is obtainable at http://www.byte.com/bmark/bmark.htm
- Linux adaptation written by Uwe F. Mayer <mayer@tux.org>


## v1.1 Source code obtained - 1996/12/14 

- Source code obtained from the BYTE website [http://www.byte.com/bmark/bmark.htm](http://www.byte.com/bmark/bmark.htm)
- Updated to work better on 64-bit machines


### v1.0.7 Memory allocation - 10/95

- Added memory array & alignment; moved memory allocation out of LU Decomposition -- RG

### v1.0.6 LU decomposition memory leak fixed - 3/95

- Fixed memory leak in LU decomposition.  Did not invalidate previous results, just made it easier to run.--RG
- Added `TOOLHELP.DLL` timing routine to Windows timer. --RG


### v1.0.5 Better naming of #defines - 1/95

- Re-did all the #defines so they made more sense.  See NMGLOBAL.H -- RG


### v1.0.4 Added timing for Macintosh - 1/95

- Added Mac time manager routines for more accurate timing on Macintosh (said to be good to 20 usecs) -- RG


### v1.0.3 Added index values - 12/94

- Added routines to calculate and display index values. Indexes based on DELL XPS 90 (90 MHz Pentium).

### v1.0.2 Bugfix integer routines - 12/94

- Bug discovered in some of the integer routines (IDEA, Huffman,...).  Routines were not accurately counting the number of loops.  Fixed. --RG (Thanks to Steve A.)


### v1.0.1 First beta by Rick Grehan, BYTE Magazine --RG - 9/94

## v1.0 Initial release, first working suite - 1993/12/03 

The team at BYTE magazine was working on this benchmark collection for a while. See the [README.nonlinux](https://github.com/kreier/nbench/blob/master/README.nonlinux) this dates back to at least December 3rd, 1993.

## Contributors

- 12/1993 - 10/1995 Rick Grehan, BYTE Magazine
- 11/1997 Andrew D. Balsa (Index-split )
- 12/1996 - 02/2003 Uwe F. Mayer (Linux/Unix* port b)
