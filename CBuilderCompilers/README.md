# C++Builder's Compilers Performance Analysis
This topic will show some HydroByte internal experience with C++Builder's compilers performance.

## Application
Tests were ran with an C++ console application called `HydroChannel`.

`HydroChannel` is an application that solves typical open channel design problems. One of the most intensive calculation modules solves the problem of a channel connecting two reservoirs. It produces a table called `Delivery Curve`. For each cell from this table, the computational solution involves a non deterministic and iterative solution of a differential equation guided by an optimization root-find model based on Newton's method.

## Code
- 13 CPP units with 4902 LOC.
- 1 Object Pascal unit with 1862 LOC.
- Total of 6764 LOC.

## Compilers
- bcc32: Windows 32-bits Classic (Borland) Compiler.
- bcc32c: Windows 32-bits Old Clang Toolchain.
- bcc64: Windows 64-bits Old Clang Toolchain.
- bcc64x: Windows 64-bits New Clang Toolchain (C++Builder 12.2).

## IDE
- C++Builder 12.2.2 (+Patch).

## Machine
- Intel i5-8250U 1.66 GHz Base, 3.40 GHz TurboBoost (4 cores, 8 threads).
- 8 Gb RAM.
- Windows 11 23H2 (22631.4460).

## Compilation tests

Build            | bcc32     | bcc32c   | bcc64    | bcc64x   |
:----------------|----------:|---------:|---------:|---------:|
`Release`        |    2.77 s |  26.23 s |  26.63 s |  11.77 s |
`Release + TC`   |    3.43 s |   9.59 s |  10.34 s |  14.33 s |

- Average time for 4 repetitions and the worst was ruled out.
- TC: TwineCompile 5.8
- bcc64x: Build dialog does not show compilation progress properly (freezes).


## Execution tests

Tested a `Delivery Curve` computation with 21 collumns and 532 rows that represents the solution of 11178 iterative `Reservoir-Channel-Reservoir` discharge problems.

Build            | bcc32     | bcc32c   | bcc64    | bcc64x   |
:----------------|----------:|---------:|---------:|---------:|
`Release`        |   2.005 s |  1.026 s |   .735 s |   .448 s |

- Average time for 4 repetitions and the worst was ruled out.