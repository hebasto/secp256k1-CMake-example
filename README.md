This is a DEMO repository with examples of using the [`libsecp256k1`](https://github.com/bitcoin-core/secp256k1)
library in downstream projects with CMake.

Source code is borrowed from https://github.com/bitcoin-core/secp256k1/tree/master/examples directly.

---

There are multiple options to use the `libsecp256k1` library in your project:
- install it into your system,
- have its source code as a subtree in your project's source tree,
- use the `FetchContent` module.


## Installed library

Switch to the ["main"](https://github.com/hebasto/secp256k1-CMake-example/tree/main) branch of this repository.


To build a binary, use commands as follows:
```sh
cmake -B build
cmake --build build
```

If the `secp256k1` library has been installed in a non-standard path, add its installation prefix to `CMAKE_PREFIX_PATH`.
For example:
```sh
cmake -B build -DCMAKE_PREFIX_PATH=/home/username/custom_lib
cmake --build build
```

## Library in a subtree

Switch to the ["subtree"](https://github.com/hebasto/secp256k1-CMake-example/tree/subtree) branch of this repository.

```sh
dir=$(mktemp -d)
cmake -B build -DCMAKE_INSTALL_PREFIX=$dir
cmake --build build --target install
tree $dir
$dir/bin/example
```

## Using `FetchContent` module

Switch to the ["fetch"](https://github.com/hebasto/secp256k1-CMake-example/tree/fetch) branch of this repository.

```sh
dir=$(mktemp -d)
cmake -B build -DCMAKE_INSTALL_PREFIX=$dir
cmake --build build --target install
tree $dir
$dir/bin/example
```
