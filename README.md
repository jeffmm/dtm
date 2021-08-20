# dtmpy

A Python module for doing fast Dynamic Topic Modeling.

This module wraps the original C code by David M. Blei and Sean M. Gerrish.

I've reorganized their code to create a static library that can be referenced by pybind11 to create Python bindings.

## Usage

Reference the DTM docstring for all possible keyword arguments.

```
import dtmpy

# Initialize DTM model flags
dtm = dtmpy.DTM(ntopics=10, corpus_prefix="path/to/seq_and_mult_files", outname="model_outputs")

# Fit the model and write outputs
dtm.fit()
```

## Requirements

- `libgsl-dev`
- `pybind11`

# Dynamic Topic Models and the Document Influence Model

This implements topics that change over time (Dynamic Topic Models) and a model of how individual documents predict that change.

This code is the result of work by David M. Blei and Sean M. Gerrish.

(C) Copyright 2006, David M. Blei

(C) Copyright 2011, Sean M. Gerrish

It includes software corresponding to models described in the
following papers:

[1] [D. Blei and J. Lafferty. Dynamic topic models. In
Proceedings of the 23rd International Conference on Machine Learning, 2006.](http://www.cs.columbia.edu/~blei/papers/BleiLafferty2006a.pdf)

[2] [S. Gerrish and D. Blei. A Language-based Approach to Measuring
Scholarly Impact. In Proceedings of the 27th International Conference
on Machine Learning, 2010.](http://www.cs.columbia.edu/~blei/papers/GerrishBlei2010.pdf)

These files are part of DIM.

DIM is free software; you can redistribute it and/or modify it under
the terms of the GNU General Public License as published by the Free
Software Foundation; either version 2 of the License, or (at your
option) any later version.

DIM is distributed in the hope that it will be useful, but WITHOUT
ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or
FITNESS FOR A PARTICULAR PURPOSE. See the GNU General Public License
for more details.

You should have received a copy of the GNU General Public License
along with this program; if not, write to the Free Software
Foundation, Inc., 59 Temple Place, Suite 330, Boston, MA 02111-1307
USA

---

A. COMPILING

You will need to have several libraries installed to compile this
package:
gsl
gflags

Depending on your package manager, you may be able to install these
with _one_ of the following commands:

sudo apt-get install libgsl0-dev libgflags-dev # Ubuntu, Debian
sudo zypper install gflags-devel gsl-devel # OpenSUSE
sudo dnf install gflags-devel gsl-devel # Fedora, CentOS

You can make the main program by changing your working directory to
dtm/ and typing:

make

This software has been compiled on Ubuntu 10.04, OpenSUSE 11.2,
CentOS 5.5, and Fedora 27. Depending on your environment, you may need to
install additional libraries.

B. RUNNING

Once everything is compiled, you can run this software by typing the
command "./main <flags>", where flags is a list of command-line
options. An example command and a description of the input and output
files is given in dtm/sample.sh. You can see all command-line options
by typing

./main --help

(although we suggest you start out with the example in dtm/sample.sh).

You should also replace 'main' by the appropriate executable (depending
on your computer architecture and operating system). We currently
provide binaries for Linux (dtm-linux32 and dtm-linux64), MacOS (dtm-darwin64)
and Windows (dtm-win32.exe and dtm-win64.exe).

C. SUPPORT and QUESTIONS

This software is provided as-is, without any warranty or support,
WHATSOEVER. If you have any questions about running this software,
you can post your question to the topic-models mailing list at
topic-models@lists.cs.princeton.edu. You are welcome to submit
modifications or bug-fixes of this software to the authors, although
not all submissions may be posted.

D. USAGE

This progam takes as input a collection of text documents and creates
as output a list of topics over time, a description of each document
as a mixture of these topics, and (possibly) a measure of how
"influential" each document is, based on its language.

We have provided an example dataset, instructions for formatting input
data and processing output files, and example command lines for
running this software in the file dtm/sample.sh.

E. CHANGES

Changes in this version include:

- Change the default top_obs_var flag to 0.5 (from -1.0)
- Change to use more iterations and a tighter convergence criterion in each doc's E-step.
- Change to initialize random topics to be a bit more "flat".
