# numba

`numba` is a python just-in-time compiler that can optimise certain operations such as basic arithmetic/matrix operations, loops, arrays, and many numpy operations. &#x20;

`numba` is a powerful module, but its documentation can be hard to follow, and is very particular about how it needs functions (return values and arguments) and variables to be defined and called. It's best to always define the type of variables, e.g. uint8 for unsigned 8-bit integer, or int64 for signed 64-bit integer.&#x20;

As shown in the below example, standard python function and variable annotations are not supported by `numba`; however the variable type of locals and function signature (parameters and return value) can be supplied to the `@jit`  decorator as shown below.

The `nopython=True` keyword argument should also always be supplied to the `@jit` decorator to make sure that python object mode is not enabled, as it can be tens or hundreds of times slower.

Whether `numba` is faster or slower than Cython or other alternatives depends on many factors, such as whether the `parallel=True` parameter is enabled and a CUDA or ROCm-enabled graphics card is available, or whether certain matrix operations can be sped up by using special CPU instructions etc.

## Numpy array support

`numba` does not support creating numpy arrays in `nopython` mode, but it can work with the underlying memory of numpy arrays which are passed to its constructor.

In order to do this, the `dtype` of the numpy array must be specified when creating the array, and the dimensions and type of the array must also be supplied in the `locals` and/or `signature_or_function` argument of the `@jit` decorator.&#x20;

Slices indicate an extra dimension. For example, `uint16[:][:]` indicates a numpy array of 2 dimensions having a type of a 16 bit unsigned integer.

Note: in order to increase speed, some of the usual memory bounds checks are not performed when accessing numpy items by index. As a result, assigning to or accessing items outside of the allocated area can cause a program crash.

## Typed List/Dict

[Typed list support](https://numba.pydata.org/numba-doc/dev/reference/pysupported.html#typed-list) (via `numba.typed.List`) can provide relatively fast operations when working with them, but when returned they may need to be converted to python lists to e.g. be encodable by the standard python `json` module or unpacked to be able to be converted to the `bytes` or `str` types etc.&#x20;

These kinds of operations can be very slow. For this reason, it may be useful to use typed lists for e.g. instances where they need to be created inside `nopython` functions (as creating numpy arrays in `nopython` `numba` functions is not supported), but it may be best to stick with numpy arrays because of them having larger numbers of use cases.

## Example

The following example is a "Run Length Encoding" algorithm that encode in pairs: the first number is the number itself, and the second number is how many times to repeat that number. This can be useful as a high-performance (but usually not particularly efficient) compression algorithm.

```python
import numpy
from PIL import Image
from numba import jit, uint8, uint64


@jit(nopython=True,
     # Indicate a function with parameters of two arrays with unsigned 
     # 8-bit integers and one unsigned 64-bit integer; and returns 
     # an unsigned 64-bit integer
     signature_or_function=uint64(uint8[:], uint8[:], uint64),
     locals={'current_item': uint8,
             'current_count': uint8,
             'y': uint64,
             'x': uint64})
def run_length_encode(out_array, in_array, num_items):
    current_item = 255
    current_count = 0
    y = 0

    for x in range(num_items):
        item = in_array[x]

        if item == current_item and current_count < 255:
            # Same item
            current_count += 1
        elif current_item == 255:
            # First item
            current_item = item
            current_count = 1
        else:
            out_array[y] = current_item
            y += 1
            out_array[y] = current_count
            y += 1

            current_item = item
            current_count = 1

    if current_item != 255:
        out_array[y] = current_item
        y += 1
        out_array[y] = current_count
        y += 1

    return y


def do_run_length_encode(in_array):
    # Allocate the numpy array before sending it to the function, 
    # as it can't be allocated while it's being run 
    out_array = numpy.ndarray(shape=(in_array.shape[0]*2,),
                              dtype=numpy.uint8)
    y = run_length_encode(out_array, in_array, in_array.shape[0])
    data = out_array[:y].tobytes()
    return data
    

if __name__ == '__main__':
    # Note that the dtype must be supplied here
    print(do_run_length_encode(numpy.array([5, 5, 5, 1, 6, 55, 55], 
                                           dtype=numpy.uint8)))
```
