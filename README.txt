=========
latex2edx
=========

Converts latex to edX XML format.

Uses plasTeX

Installation
============

    pip install -e git+https://github.com/mitocw/latex2edx.git#egg=latex2edx

Note that xmllint and lxml are required; for ubuntu, this may work:

    apt-get install libxml2-utils python-lxml

Usage
=====

Usage: latex2edx [options] filename.tex

Options:

  --version             show program's version number and exit
  -h, --help            show this help message and exit
  -v, --verbose         verbose error messages
  -o OUTPUT_FN, --output-xbundle=OUTPUT_FN
                        Filename for output xbundle file
  -d OUTPUT_DIR, --output-directory=OUTPUT_DIR
                        Directory name for output course XML files
  -c CONFIG_FILE, --config-file=CONFIG_FILE
                        configuration file to load
  -m, --merge-chapters  merge chapters into existing course directory

Example
=======

See live demo course: https://edge.edx.org/courses/MITx/MIT.latex2edx/2014_Spring/about

The source code for the demo course is here: https://github.com/mitocw/content-mit-latex2edx-demo

Here is an annotated input tex file which generates the source for an edX course:

    %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
    \documentclass[12pt]{article}
    
    \usepackage{edXpsl}	% edX "problem specification language"
    
    \begin{document}
    
    % edXcourse: {course_number}{course display_name}[optional arguments like semester]
    \begin{edXcourse}{MIT.latex2edx}{latex2edx demo course}[semester="2014 Spring"]
    
    % edXchapter: {chapter display_name}[optional arguments like url_name]
    \begin{edXchapter}{Basic examples}
    
    % edXsection: {section display_name}[optional arguments like url_name]
    % this turns into a <sequential> in the XML
    \begin{edXsection}{Basic example problems}
    
    % edXvertical: {vertical display_name}[optional arguments like url_name]
    \begin{edXvertical}
    
    % edXproblem: {problem display_name}{attributes: url_name, weight, attempts}
    \begin{edXproblem}{Numerical response}{attempts=10}
    
    What is the numerical value of $\pi$?

    % \edXabox: answer box, specifying question type and expected response
    \edXabox{expect="3.14159" type="numerical" tolerance='0.01' }
    
    \end{edXproblem}
    \end{edXvertical}
    \end{edXsection}
    \end{edXchapter}
    \end{edXcourse}
    \end{document}
    
    %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

History
=======

* v1.0: python package; unit tests; xbundle and modular code
* v1.1.0: Support for jsinput, custom mathjax filtering, formularesponse
*     .1: Fix optargs bug with plastex
*     .2: Allow spaces in semester; give example in README
*     .3: Fix bug in eqnarray table widths
