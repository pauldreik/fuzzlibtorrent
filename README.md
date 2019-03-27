locally, run
mkdir build
cd build
CC=clang-5.0 CXX=clang++-5.0 LIB_FUZZING_ENGINE=/usr/lib/llvm-5.0/lib/libFuzzer.a cmake  ..

to make sure the scripts work.

