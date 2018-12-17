# Triton

Copyright (c) 2018 Triton Developers.   
Copyright (c) 2014-2018 The Monero Project.     
Portions Copyright (c) 2012-2013 The Cryptonote developers.

## Contact
Mail : tritonix.project@gmail.com

## Introduction
Triton is a Monero forked cryptocurrency which focuses on decentralization. It comes with all features Monero has, including Bulletproofs. To ensure the resistance to ASICs, Triton will follow Monero's mining algorithm updates which occurs every 6 months.
The purpose of Triton's development is to show how a digital currency can be a peer to peer electronic cash for the whole world and at the same time, a decentralized system. More specifically,  mining hash power distribution, which will lead to decentralized block creation.
In order to do this, we will make a few changes in the mining protocol. No details will be written here, but basically, this modified mining protocol will make it extremely difficult to collaborate with other miners to mine blocks, which we believe, will lead to a more secure network.

## Build
### Install dependencies

Debian / Ubuntu one liner for all dependencies  
` sudo apt update && sudo apt install build-essential cmake pkg-config libboost-all-dev libssl-dev libzmq3-dev libunbound-dev libsodium-dev libunwind8-dev liblzma-dev libreadline6-dev libldns-dev libexpat1-dev doxygen graphviz libpgm-dev`

### Cloning the repository
Clone recursively to pull-in needed submodule(s):

`$ git clone --recursive https://github.com/tritonix/triton`

If you already have a repo cloned, initialize and update:

`$ cd triton && git submodule init && git submodule update`

### Build instructions

Triton uses the CMake build system and a top-level [Makefile](Makefile) that
invokes cmake commands as needed.

#### On Linux and OS X

* Build:
```     
        $ mkdir build
        $ cd build
        $ cmake ..
        $ make
```
    *Optional*: If your machine has several cores and enough memory, enable
    parallel build by running `make -j<number of threads>` instead of `make`. For
    this to be worthwhile, the machine should have one core and about 2GB of RAM
    available per thread.

    *Note*: If cmake can not find zmq.hpp file on OS X, installing `zmq.hpp` from
    https://github.com/zeromq/cppzmq to `/usr/local/include` should fix that error.

* The resulting executables can be found in `build/bin`

* Add `PATH="$PATH:$HOME/triton/build/bin"` to `.profile` (optional)

* Run Triton with `tritond --detach`

Dependencies need to be built with -fPIC. Static libraries usually aren't, so you may have to build them yourself with -fPIC. Refer to their documentation for how to build them.

* **Optional**: build documentation in `doc/html` (omit `HAVE_DOT=YES` if `graphviz` is not installed):

        HAVE_DOT=YES doxygen Doxyfile

## Installing Triton from a package

## Running tritond

The build places the binary in `bin/` sub-directory within the build directory
from which cmake was invoked (repository root by default). To run in
foreground:

    ./bin/tritond

To list all available options, run `./bin/tritond --help`.  Options can be
specified either on the command line or in a configuration file passed by the
`--config-file` argument.  To specify an option in the configuration file, add
a line with the syntax `argumentname=value`, where `argumentname` is the name
of the argument without the leading dashes, for example `log-level=1`.

To run in background:

    ./bin/tritond --log-file tritond.log --detach

To run as a systemd service, copy
[tritond.service](utils/systemd/tritond.service) to `/etc/systemd/system/` and
[tritond.conf](utils/conf/tritond.conf) to `/etc/`. The [example
service](utils/systemd/tritond.service) assumes that the user `triton` exists
and its home is the data directory specified in the [example
config](utils/conf/tritond.conf).

If you're on Mac, you may need to add the `--max-concurrency 1` option to
triton-wallet-cli, and possibly tritond, if you get crashes refreshing.

## License
See [LICENSE](LICENSE).
