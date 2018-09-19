# C++ make 
# standard compile options for the c++ executable
FLAGS = -fPIC

# the python interface through swig
PYTHONI = -I/usr/include/python2.7
PYTHONL = -Xlinker -export-dynamic

_example.so : example.o example_wrap.o
	g++ $(PYTHONL) $(LIBFLAGS) -shared example.o example_wrap.o -o _example.so

example.o : example.cpp
	g++ $(FLAGS) -c example.cpp

example_wrap.o : example_wrap.cxx
	g++ $(FLAGS) $(PYTHONI) -c example_wrap.cxx

example_wrap.cxx example.py : example.i example.h
	swig -c++ -python example.i

clean:
	rm -f *.out *.o *.so example_wrap.* example.py* *.swp
	rm -rf __pycache__

test:
	/usr/bin/python test.py

all: _example.so test

.PHONY: clean test all

.DEFAULT_GOAL := all
