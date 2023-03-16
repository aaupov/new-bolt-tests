# new-bolt-tests
This is testsuite containing binary tests for 
[BOLT](https://github.com/llvm/llvm-project/tree/main/bolt).

## Usage
### Prerequisites
- Install binary tests prerequisites:
```
sudo apt install libtinfo5 zstd curl
```
- Install perf tools:
```
sudo apt-get install linux-tools-`uname -r`
```
### LLVM CMake configuration
Configure LLVM with the `LLVM_EXTERNAL_PROJECTS` and
`LLVM_EXTERNAL_PROJECTS_SOURCE_DIR` cmake flags. Example:

```
$ git clone https://github.com/llvm/llvm-project
$ git clone https://github.com/aaupov/new-bolt-tests
$ cmake -B bolt-build -G Ninja llvm-project/llvm \
   -DCMAKE_BUILD_TYPE=Release \
   -DLLVM_TARGETS_TO_BUILD="X86;AArch64" \
   -DLLVM_ENABLE_PROJECTS="clang;lld;bolt" \
   -DLLVM_EXTERNAL_PROJECTS="bolttests" \
   -DLLVM_EXTERNAL_BOLTTESTS_SOURCE_DIR=$(pwd)/new-bolt-tests
$ cmake --build bolt-build --target check-large-bolt
```

When this repo is configured as an external project, it will add itself as an
extra target in LLVM named "check-large-bolt". Just build that target to run
this testsuite.
