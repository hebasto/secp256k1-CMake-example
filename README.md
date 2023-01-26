This is a DEMO repository with examples of using an installed [`secp256k1`](https://github.com/bitcoin-core/secp256k1)
library with [CMake](https://github.com/bitcoin-core/secp256k1/pull/1113).

Source code is borrowed from https://github.com/bitcoin-core/secp256k1/tree/master/examples directly.

To build a binary, use commands as follows:
```sh
cmake -S . -B build
cmake --build build
```

If the `secp256k1` library has been installed in a non-standard path, add its installation prefix to `CMAKE_PREFIX_PATH`.
For example:
```sh
cmake -S . -B build -DCMAKE_PREFIX_PATH=/home/username/custom_lib
cmake --build build
```
