Sloc Cloc and Code (scc)
------------------------

A tool similar to cloc, sloccount and tokei. For counting physical the lines of code, blank lines, comment lines, and physical lines of source code in many programming languages.

Goal is to be the fastest code counter possible, but also perform COCOMO calculation like sloccount and to estimate code complexity similar to cyclomatic complexity calculators. In short one tool to rule them all and the one I wish I had before I wrote it.

Also it has a much shorter name than tokei, and shorter than cloc.

[![Build Status](https://travis-ci.org/boyter/scc.svg?branch=master)](https://travis-ci.org/boyter/scc)

Dual-licensed under MIT or the [UNLICENSE](http://unlicense.org).

Read all about how it came to be https://boyter.org/posts/sloc-cloc-code/

Other similar projects,

 - https://github.com/Aaronepower/tokei
 - https://github.com/AlDanial/cloc
 - https://www.dwheeler.com/sloccount/
 - https://github.com/cgag/loc
 - https://github.com/hhatto/gocloc/
 - http://www.locmetrics.com/alternatives.html

Interesting reading about about code counting
 - https://www.reddit.com/r/rust/comments/59bm3t/a_fast_cloc_replacement_in_rust/
 - https://www.reddit.com/r/rust/comments/82k9iy/loc_count_lines_of_code_quickly/

Futher reading about processing files on the disk performance
 - https://blog.burntsushi.net/ripgrep/


### Usage

Command line usage of `scc` is designed to be as simple as possible.
Full details can be found in `scc --help`.

```
$ scc --help
NAME:
   scc - Sloc, Cloc and Code. Count lines of code in a directory with complexity estimation.

USAGE:
   scc DIRECTORY

VERSION:
   1.0.0

COMMANDS:
     help, h  Shows a list of commands or help for one command

GLOBAL OPTIONS:
   --pathblacklist value, --pbl value  Which directories should be ignored as comma seperated list (default: ".git,.hg,.svn")
   --sort value, -s value              Sort languages / files based on column [possible values: files, name, lines, blanks, code, comments, complexity] (default: "files")
   --whitelist value, --wl value       Restrict file extensions to just those provided as a comma seperated list E.G. go,java,js
   --files                             Set to specify you want to see the output for every file
   --verbose, -v                       Set to enable verbose output
   --duplicates, -d                    Set to check for and remove duplicate files from stats and output
   --wide, -w                          Set to check produce more output such as code vs complexity ranking
   --averageage value, --aw value      Set as integer to set the average wage used for basic COCOMO calculation (default: 56286)
   --cocomo, --co                      Set to check remove cocomo calculation output
   --debug                             Set to enable debug output
   --trace                             Set to enable trace output, not reccomended for multiple files
   --help, -h                          show help
   --version, --ver                    Print the version
```

Output should look something like the below for the redis project

```
$ scc .
-------------------------------------------------------------------------------
Language                 Files     Lines     Code  Comments   Blanks Complexity
-------------------------------------------------------------------------------
C                          215    114488    85341     15175    13972      21921
C Header                   144     20042    13308      4091     2643       1073
TCL                         93     15702    12933       922     1847       1482
Lua                         20       524      384        71       69         66
Autoconf                    18     10713     8164      1476     1073        986
Shell                       18       810      513       196      101        102
Makefile                     9      1021      716       100      205         50
Ruby                         8      2416     1798       376      242        365
HTML                         6     11472     8288         5     3179        548
Markdown                     6      1312      964         0      348          0
CSS                          2       107       91         0       16          0
YAML                         2        75       60         4       11          4
C++ Header                   1         9        5         3        1          0
C++                          1        46       30         0       16          5
Batch                        1        28       26         0        2          3
Plain Text                   1       499      499         0        0          0
-------------------------------------------------------------------------------
Total                      545    179264   133120     22419    23725      26605
-------------------------------------------------------------------------------
Estimated Cost to Develop $4,592,517
Estimated Schedule Effort 27.382310 months
Estimated People Required 19.867141
-------------------------------------------------------------------------------
```

### Tests

scc is pretty well tested with many unit, integration and benchmarks to ensure that it is fast and complete.

### Package

Run go build for windows and linux then the following in linux, keep in mind need to update the version

```
zip -r9 lc-1.0.0-x86_64-pc-windows.zip lc.exe && zip -r9 lc-1.0.0-x86_64-unknown-linux.zip lc

GOOS=darwin GOARCH=amd64 go build && zip -r9 scc-1.0.0-x86_64-apple-darwin.zip scc
GOOS=windows GOARCH=amd64 go build && zip -r9 scc-1.0.0-x86_64-pc-windows.zip scc.exe
GOOS=linux GOARCH=amd64 go build && zip -r9 scc-1.0.0-x86_64-unknown-linux.zip scc
```


### Releases

1.0.1
 - Add ability to disable the parallel file walker through command line option https://github.com/boyter/scc/issues/1

1.0.0 
 - First release