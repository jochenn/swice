(C) 2014 Jochen Schlobohm, jochen.schlobohm@gmail.com

========== SWig Inline C ==========

This project makes it possible to use c-code inside python code. It is inspired by weave but tries to keep it as simple as possible.

The code relies on swig and distutils to generate and compile the temporary module. Both have to be installed on your computer.

One example can be seen in swice.py when running as main-program.

Another Example:

```python

import swice
code = '''

	for(int i = 0; i< Na(0); i++)
		a(i) = a(i)*5;
    
'''
a = np.array([1,2,3,4])
swice.inline(code, ['a'], locals(), globals())

print(a) # will print [5,10,15,20]
```

<code>return_val</code> is an integer wich will be returned when invoking <code>inline()</code>

In order to find out if the given code has already been used (and therefore compiled) a hash is calculated from the generated interface and code.
If the temporary library is already present, it will just be loaded and not recompiled. Recompiling can be forced by setting the flag <code>recompile</code>.
If you change additional libraries, headers or source files without altering the code or interface, the hash algorithm will not notice. Setting <code>recompile</code> to True will help.
If the <code>extracode</code> is changed, the hash will change because it is simply copied into the main C-file.

By the way:
Integer Arrays are mapped to stdint.h -types (e.g. uint8_t instead of unsigned char)

"__g" is a forbidden identifier for your c-code and variable names.

C variable access:
Each numpy array will be accessible by a <varName>(dim1, [dim2, [...]]). The size of each dimension is stored in N<varName>[<dim>].
Scalars are copied into and from the module. 


Necessary programs and libraries:

numpy
swig
python-dev (e.g. for ubuntu)


TODOs

- additional sorce files (not tested yet)
- includes (not tested yet)
- src-dir
- libs & libdirs (not tested yet)
