# Python

{% hint style="success" %}
See also python standard library docs written by some of the same authors of this guide at [https://montutes.github.io/monpytute/](https://montutes.github.io/monpytute/)!
{% endhint %}

Python is a multipurpose programming language. It was built with certain philosophies in mind including readability - see also the output from the following when it's typed into an interpreter:

```python
>>> import this
The Zen of Python, by Tim Peters

Beautiful is better than ugly.
Explicit is better than implicit.
Simple is better than complex.
Complex is better than complicated.
Flat is better than nested.
Sparse is better than dense.
Readability counts.
Special cases aren't special enough to break the rules.
Although practicality beats purity.
Errors should never pass silently.
Unless explicitly silenced.
In the face of ambiguity, refuse the temptation to guess.
There should be one-- and preferably only one --obvious way to do it.
Although that way may not be obvious at first unless you're Dutch.
Now is better than never.
Although never is often better than *right* now.
If the implementation is hard to explain, it's a bad idea.
If the implementation is easy to explain, it may be a good idea.
Namespaces are one honking great idea -- let's do more of those!
```

It typically isn't a high-performing language and can be as much as 30x slower or more than a compiled language. However, many modules used for data processing, maths and machine learning are available which can allow batch processing as fast as, or even faster than, a compiled language like C.&#x20;

It frequently is used for:

* Quick shell scripts for system administration
* Backend REST and GraphQL APIs
* Data processing:
  * numpy, pandas (numpy for lower level arrays with optimised linear algebra operations, and collections of numpy-like arrays with pandas)
  * Machine learning (tensorflow, PyTorch, SciKit-Learn)
* High-performance and parallel computing:
  * Examples of libraries include Cython (a python to C transpiler), numba, OpenMP, ray
* Image processing (with pillow)

It can be used for:

* Web user interface development (flask, Django; although Node.js with React is much more commonly used and with more devs comes greater support and more external libraries)
* Desktop UI development (tkinter, PyQT, PyGTK, wxPython are some examples)

It less commonly is used for:

* Game development
* Video and audio processing
