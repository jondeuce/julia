                   _
       _       _ _(_)_     |
      (_)     | (_) (_)    |   A fresh approach to technical computing
       _ _   _| |_  __ _   |
      | | | | | | |/ _` |  |           http://julialang.org
      | | |_| | | | (_| |  |       julia-math@googlegroups.com
     _/ |\__'_|_|_|\__'_|  |
    |__/                   |


<a name="The-Julia-Language"/>
## The Julia Language

Julia is a high-level, high-performance dynamic language for numerical and scientific computing.
It provides a sophisticated compiler, distributed parallel execution, and numerical accuracy.
It also has easy interfaces to mature, best-of-breed C and Fortran libraries for technical computing tasks such as matrix math, random number generation, fast Fourier transforms, and string processing.
Key language features include multiple dispatch, optional typing, and excellent performance through type inference and just-in-time (JIT) compilation.
For a more in-depth discussion of the rationale and advantages of Julia over other systems, see the following highlights or read the [introduction](https://github.com/JuliaLang/julia/wiki/Introduction) in the [manual](https://github.com/JuliaLang/julia/wiki/).

### High-Performance JIT Compiler 

Julia is an interactive environment with a high performance JIT compiler, with syntax that is familiar to users of other technical computing environments.
The following [benchmarks](https://github.com/JuliaLang/julia/blob/master/test/perf.j) are from a Macbook with 2.1GHz Intel Core 2 Duo:

<table cellspacing="0" border="0">
<thead>
  <tr>
    <td/>
    <th>Julia</th>
    <th>Matlab</th>
    <th>Octave</th>
    <th>Python/NumPy</th>
    <th>C++ (GCC)</th>
  </tr>
  <tr>
    <td/>
    <th>46c2c6de</th>
    <th>R2011a</th>
    <th>3.4</th>
    <th>2.7.1/1.5.1</th>
    <th>4.6.1 (-O3)</th>
  </tr>
</thead>
<tbody>
  <tr>
    <th>fib</th>
    <td align="right" width="80px">      .500 </td>
    <td align="right" width="80px">   309.000 </td>
    <td align="right" width="80px">   570.000 </td>
    <td align="right" width="80px">     7.490 </td>
    <td align="right" width="80px">      .179 </td>
  </tr>
  <tr>
    <th>parse_int</th>
    <td align="right" width="80px">      .210 </td>
    <td align="right" width="80px">   124.000 </td>
    <td align="right" width="80px">   557.000 </td>
    <td align="right" width="80px">      .630 </td>
    <td align="right" width="80px">      .151 </td>
  </tr>
  <tr>
    <th>mandel</th>
    <td align="right" width="80px">     1.820 </td>
    <td align="right" width="80px">    40.000 </td>
    <td align="right" width="80px">   260.000 </td>
    <td align="right" width="80px">     9.640 </td>
    <td align="right" width="80px">      .530 </td>
  </tr>
  <tr>
    <th>quicksort</th>
    <td align="right" width="80px">      .640 </td>
    <td align="right" width="80px">    71.000 </td>
    <td align="right" width="80px">  1611.000 </td>
    <td align="right" width="80px">    30.600 </td>
    <td align="right" width="80px">      .600 </td>
  </tr>
  <tr>
    <th>pi_sum</th>
    <td align="right" width="80px">    49.500 </td>
    <td align="right" width="80px">    69.000 </td>
    <td align="right" width="80px"> 20578.000 </td>
    <td align="right" width="80px">  1289.000 </td>
    <td align="right" width="80px">    49.300 </td>
  </tr>
  <tr>
    <th>rand_mat_stat</th>
    <td align="right" width="80px">    38.900 </td>
    <td align="right" width="80px">   139.000 </td>
    <td align="right" width="80px">   517.000 </td>
    <td align="right" width="80px">   363.000 </td>
    <td align="right" width="80px">           </td>
  </tr>
</tbody>
</table>

Relative performance between languages on Linux is similar.
These benchmarks, while not comprehensive, do test compiler performance on a range of common code patterns, such as function calls, string parsing, sorting, numerical loops, random number generation, and array operations.

*Note:* A C++ implementation of random matrix statistics is missing because this test involves many whole-matrix operations, and it is not clear what an idiomatic implementation would look like.

### Designed for Parallelism

Julia does not impose any particular style of parallelism on the user.
Instead, it is flexible enough to support a number of styles of [parallelism](https://github.com/JuliaLang/julia/wiki/Parallel-Computing), and makes it easy for the user to add more.
The following simple example demonstrates how to count the number of heads in a large number of coin tosses in parallel.

    nheads = @parallel (+) for i=1:100000000
      randbit()
    end

This computation is automatically distributed across all available nodes participarting in the computation session, and the result, reduced by summation (`+`), is returned at the calling node.
It is also possible to add and remove compute nodes while a session is running, allowing elasticity and fault recovery.

### Free, Open Source & Library-Friendly

The core of the Julia implementation is licensed under the [MIT license][MIT].
Various libraries used by the Julia environment include their own licenses such as the [GPL], [LGPL], and [BSD] (therefore the environment, which consists of the language, user interfaces, and libraries, is under the GPL).
Users can easily combine their own code or even proprietary third-party libraries, should they choose to.
Furthermore, Julia makes it easy to call functions from [external C and Fortran shared libraries](https://github.com/JuliaLang/julia/wiki/Calling-C-and-Fortran-Code), without writing any wrapper code, or even recompiling code.
You can try calling external library functions directly from Julia's interactive prompt, playing with the interface and getting immediate feedback until you get it right.
See [LICENSE](https://github.com/JuliaLang/julia/blob/master/LICENSE) for the full terms Julia's licensing.

[MIT]:  http://en.wikipedia.org/wiki/MIT_License
[GPL]:  http://en.wikipedia.org/wiki/GNU_General_Public_License
[LGPL]: http://en.wikipedia.org/wiki/GNU_Lesser_General_Public_License
[BSD]:  http://en.wikipedia.org/wiki/BSD_licenses

<a name="Resources"/>
## Resources

- **Homepage:** <http://julialang.org>
- **Discussion:** <julia-math@googlegroups.com>
- **Source code:** <https://github.com/JuliaLang/julia>
- **Git clone URL:** <git://github.com/JuliaLang/julia.git> (see [below](#Download-Compilation))
- **Documentation:** <https://github.com/JuliaLang/julia/wiki>

<a name="Required-Build-Tools-External-Libraries"/>
## Required Build Tools & External Libraries

- **[GNU make][]** — building dependencies.
- **[gcc, g++, gfortran][gcc]** — compiling and linking C, C++ and Fortran code.
- **[curl][]** — to automatically download external libraries:
    - **[LLVM][]**         — compiler infrastructure.
    - **[fdlibm][]**       — a portable implementation of much of the system-dependent libm math library's functionality.
    - **[MT][]**           — a fast Mersenne Twister pseudorandom number generator library.
    - **[OpenBLAS][]**     — a fast, open, and maintained [basic linear algebra subprograms (BLAS)](http://en.wikipedia.org/wiki/Basic_Linear_Algebra_Subprograms) library, based on [Kazushige Goto's](http://en.wikipedia.org/wiki/Kazushige_Goto) famous [GotoBLAS](http://www.tacc.utexas.edu/tacc-projects/gotoblas2/).
    - **[LAPACK][]**       — library of linear algebra routines for solving systems of simultaneous linear equations, least-squares solutions of linear systems of equations, eigenvalue problems, and singular value problems.
    - **[ARPACK][]**       — a collection of subroutines designed to solve large, sparse eigenvalue problems.
    - **[FFTW][]**         — library for computing fast Fourier transforms very quickly and efficiently.
    - **[PCRE][]**         — Perl-compatible regular expressions library.
    - **[GNU readline][]** — library allowing shell-like line editing in the terminal, with history and familiar key bindings.

[GNU make]:     http://www.gnu.org/software/make/
[gcc]:          http://gcc.gnu.org/
[curl]:         http://curl.haxx.se/
[fdlibm]:       http://www.netlib.org/fdlibm/readme
[MT]:           http://www.math.sci.hiroshima-u.ac.jp/~m-mat/MT/emt.html
[OpenBLAS]:     https://github.com/xianyi/OpenBLAS#readme
[LAPACK]:       http://www.netlib.org/lapack/
[ARPACK]:       http://www.caam.rice.edu/software/ARPACK/
[FFTW]:         http://www.fftw.org/
[PCRE]:         http://www.pcre.org/
[GNU readline]: http://cnswww.cns.cwru.edu/php/chet/readline/rltop.html
[LLVM]:         http://www.llvm.org/

<a name="Supported-Platforms"/>
## Supported Platforms

- **GNU/Linux:** x86/64 (64-bit); x86 (32-bit).
- **Darwin/OS X:** x86/64 (64-bit); x86 (32-bit) is untested but should work.

<a name="Download-Compilation"/>
## Download & Compilation

First, acquire the source code either by cloning the git repository (requires **[git](http://git-scm.com/)** to be installed):

    git clone git://github.com/JuliaLang/julia.git

or, if you don't have git installed, by using curl and tar to fetch and unpack the source:

    mkdir julia && curl -Lk https://github.com/JuliaLang/julia/tarball/master | tar -zxf- -C julia --strip-components 1

Next, enter the `julia/` directory and run `make` to build the `julia` executable.
When compiled the first time, it will automatically download and build its [external dependencies](#Required-Build-Tools-External-Libraries).
This takes a while, but only has to be done once.

No installation is required; `julia` is currently run from the directory where it was built.
You might, however, want to make a symbolic link for the executable, for example `ln -s JULIA_PATH/julia ~/bin/julia`.
Please note that the build process will not work if any of the build directory's parent directories have spaces in their names (this is due to a limitation in GNU make).

Congratulations, if you've gotten this far, you are ready to try out Julia.
You can read about [getting started](https://github.com/JuliaLang/julia/wiki/Getting-Started) in the manual.

<a name="Directories"/>
## Directories

    attic/         old, now-unused code
    contrib/       emacs and textmate support for julia
    doc/           miscellaneous documentation and notes
    examples/      example julia programs
    external/      external dependencies
    j/             source code for julia's standard library
    lib/           shared libraries loaded by julia's standard libraries
    src/           source for julia language core
    test/          unit and function tests for julia itself
    ui/            source for various front ends

<a name="Emacs-Setup"/>
## Emacs Setup

Add the following line to `~/.emacs`

    (require 'julia-mode "JULIA_PATH/contrib/julia-mode.el")

where `JULIA_PATH` is the location of the top-level julia directory.

<a name="TextMate-Setup"/>
## TextMate Setup

Copy (or symlink) the TextMate Julia bundle into the TextMate application support directory:

    cp -r JULIA_PATH/contrib/Julia.tmbundle ~/Library/Application\ Support/TextMate/Bundles/

where `JULIA_PATH` is the location of the top-level julia directory.
Now select from the menu in TextMate `Bundles > Bundle Editor > Reload Bundles`.
Julia should appear as a file type and be automatically detected for files with the `.j` extension.
