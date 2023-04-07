# PyPy

PyPy is a Just-in-Time compiler alternative implementation to CPython.&#x20;

It often can be orders of magnitude faster than CPython for pure python code. See also the benchmarks at [https://speed.pypy.org/](https://speed.pypy.org/) for current numbers.

However, when calling python modules written in C performance can be much slower than CPython, if they work at all. See also [http://packages.pypy.org/](http://packages.pypy.org/) for which modules are currently supported by PyPy.

It's worth noting that future versions of CPython may be much faster (as of this edit) as at [https://github.com/markshannon/faster-cpython/blob/master/plan.md](https://github.com/markshannon/faster-cpython/blob/master/plan.md).
