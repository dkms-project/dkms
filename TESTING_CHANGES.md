# Testing DKMS

Testing changes to the code can be easily performed by extending the provided `run_tests.sh` script and executing the tests locally before submitting. These tests can be performed on a VM, in a `chroot` or in a container.

It's not recommended to run the tests on the same system you need to have functional DKMS modules, so please create a dedicated environment for this.

## Prerequisites

First of all, make sure you have compiler, kernel development headers and all the tools required to build modules on your system. Installing a DKMS package provided by your distribution is a good way to make sure all the dependencies are already in place.

After this preparatory step; install the DKMS snapshot or version that contains the changes you want to test:

```
$ make
$ sudo make install
```

## Running tests

To run all tests with the local kernel:

```
$ sudo KERNEL_VER=$(uname -r) ./run_test.sh
```

## Running selective tests

The full test suite is quite extensive and can take very long to execute. To speed up, you can only execute the "block" of tests that are of interest for your changes.

By running a `grep only` on the `run_test.sh` script, we can see what are the targets that can be used. After picking the appropriate target (for exmple the `broken` section to test malformed modules), you can just run the exclusive tests pertaining to that section:

```
$ sudo KERNEL_VER=$(uname -r) ./run_test.sh broken
```

## Cleaning up

After making all the changes necessary to test new features, you can clean up the system with the following commands:

```
$ sudo make uninstall
