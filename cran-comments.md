---
title: "Cran Comments"
author: "Ivan Svetunkov"
date: "12 January 2021"
output: html_document
---
## Version
This is ``smooth`` package, v3.0.1.

## Update from the previous submission
I've added skip_on_cran() for the majority of tests now, which should reduce the computational time.
I plan to merge some of C++ functions in future releases, so that the compilation will take less time.

## Test environments
* local ubuntu 20.04, R 4.0.3
* ubuntu 16.04.6 (on travis-ci), R 4.0.3
* win-builder (devel and release) - see a comment below
* rhub with rhub::check_for_cran() command

## R CMD check results
R CMD check results
checking installed package size ... NOTE
     installed size is 28.7Mb
     sub-directories of 1Mb or more:
       R      1.3Mb
       doc    3.9Mb
       libs  23.0Mb
0 errors | 0 warnings | 1 note

## win-builder check results
>* checking package dependencies ... NOTE
>Package suggested but not available for checking: 'doMC'

This is expected, because doMC is not available for Windows.

I had to remove almost all examples in the adam() function, because they were working too slow for some reason. In reality the function is faster than the v3.0.0

## rhub checks
### Windows Server 2008 R2 SP1, R-devel, 32/64 bit
> Package suggested but not available: 'doMC'
> The suggested packages are required for a complete check.
    
This is because doMC is not available for Windows.

### Debian Linux, R-devel, GCC ASAN/UBSAN
Gives PREPERROR because `dependencies ‘greybox’, ‘forecast’ are not available for package ‘smooth’`. This does not have any explanation, because both packages are available on CRAN.

Everything was checked without major issues. The only thing is a note about the installed package size for different platforms (similar to R CMD check results).

## Downstream dependencies
I have also run R CMD check on reverse dependencies of smooth.
No ERRORs or WARNINGs found.
