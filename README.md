# sha256 #

Hardware implementation of the SHA-256 cryptographic hash function with
support for SHA-256. The original implementation is
written in Verilog 2001 compliant code. This fork is written in Xilinx
System Verilog as implemented in Vivado 2017.2 and later.  The
implementation includes the main core as well as wrappers that provides
interfaces for simple integration.

This is a low area implementation that iterates over the rounds but
there is no sharing of operations such as adders.

The hardware implementation is complemented by a functional model
written in Python.


## Implementation status ##

The original core has been completed for a long time and been used in
several designs in ASICs as well as in FPGAs. The core is mature and
ready for use. Minor changes are non-functional cleanups of code.

This fork has been implented in Xilinx UltraScale and UltraScale+
FPGAs.


## Implementation details ##

The sha256 design is divided into the following sections.
- src/rtl - RTL source files
- src/tb  - Testbenches for the RTL files
- src/model/python - Functional model written in python
- doc - documentation (currently not done.)
- toolruns - Where tools are supposed to be run.

The actual core consists of the following files:
- sha256_core.sv - The core itself with wide interfaces.
- sha256_w_mem.sv - W message block memory and block expansion logic.
- sha256_k_constants.sv - K constants ROM memory.

The top level entity is called sha256_core. This entity has wide
interfaces (512 bit block input, 256 bit digest). In order to make it
usable you probably want to wrap the core with a bus interface.

The provided top level wrapper, sha256.sv provides a simple 32-bit memory
like interface. The core (sha256_core) will sample all data inputs when
given the init or next signal. the wrapper contains additional data
registers. This allows you to load a new block while the core is
processing the previous block.


## ASIC-results ##


## Fpga-results ##

### Xilinx FPGAs ###
Implementation results using Vivado 2017.2.

**UltraScale Virtex**
- XCVU125-FLVB2104-2-E


## TODO ##
- Complete documentation.
