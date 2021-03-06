[![Build Status](https://travis-ci.org/dbeurle/imr.svg?branch=master)](https://travis-ci.org/dbeurle/imr)
[![Coverage Status](https://coveralls.io/repos/github/dbeurle/imr/badge.svg?branch=master)](https://coveralls.io/github/dbeurle/imr?branch=master)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

# Intermediate Mesh Representation

A reader for Gmsh files for processing serial and decomposed grids.  This project is a command line interface (CLI) program and is designed to perform the off-line conversion of serial and decomposed grids into separate `JSON` mesh files.  These files can be readily imported into a numerical analysis program using `JSON` readers avoiding dealing with the format of `.msh` files.

![alt text](https://github.com/dbeurle/imr/blob/master/doc/images/feti.png "FETI example")

# Building

This project uses CMake as the build system and can be built out-of-tree using:
* `mkdir build && cd build`
* `cmake -DCMAKE_BUILD_TYPE=Release ..`
* `make all`

Optionally, you can also install the binary to a system location by

* `make install`

# Gmsh file format

Gmsh specifies information tags and the nodal connectivity for each element.  When a mesh is partitioned, for example with two partitions, the information tags would have the following data:

| 10 | 2 | 5 | 1 | 6 | 2 | 2 | -1 | 5 22 4 |
| :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| element # | element type (Triangle3) | tags | physical # | geometrical # | processes | owner | ghost | `nodalConnectivity` |

GmshReader parses the file and splits the elements into groups based on their element type.  If the mesh contains partitions, then these are split into separate files so each processor can read in their respective mesh partition without parsing the original file.

# Usage

Examples of usage are available in the project directory `examples`.  There is also a command line interface with the list of command line options given by executing

* `gmshreader --help`

# Issues

If there are any issues in using the program, please open an issue using the GitHub tool above.  Bug reports, suggestions and improvements are very welcome!
