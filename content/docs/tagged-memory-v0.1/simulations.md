+++
Description = ""
date = "2015-04-12T15:39:40+01:00"
title = "Running simulations"
parent = "/docs/tagged-memory-v0.1/"
prev = "/docs/tagged-memory-v0.1/setup/"
next = "/docs/tagged-memory-v0.1/spike/"
showdisqus = true

+++


Programs can be run by first booting RISC-V Linux on the simulator or
FPGA. Alternatively, they can be run without full OS support either in
a pure bare metal mode or with the support of the 
[newlib](https://sourceware.org/newlib/)
library (a C standard library implementation) and a simple proxy kernel.

### Bare metal mode 

Programs running in this mode have no library support. The host target
interface (HTIF) must be accessed directly by the program if necessary, e.g.
to print messages on the host terminal.

 All the test cases found in
`lowrisc-chip/riscv-tools/riscv-tests/isa` are run in bare metal mode.
The success/fail status of each test is placed in the `tohost` CSR
which can be checked by the host.  For more information, see
`lowrisc-chip/riscv-tools/riscv-tests/env/p/riscv_test.h`

### Newlib/Proxy Kernel (PK)

Tests and systems not requiring access to a full-blown OS can be
compiled for use with the proxy kernel (PK) and newlib. The proxy
kernel simply proxies syscalls to the host over the host target
interface (HTIF). This provides support for commonly used functions
such as `printf()`.

The `riscv64-unknown-elf-gcc` GCC compiler produces code for use with
the PK and newlib.

### RISC-V Linux

Alternatively, programs can be run under a booted Linux system. The programs
running on Linux have the full system support, such as pthread, time,
etc. However, the running time is much longer than the previous two due to the 
requirement to boot Linux in the simulation environment.

### Running programs on the software simulators and FPGAs

Regardless of the whether programs require full Linux support or not,
simulations can take place at different levels (e.g. functional,
cycle-accurate) or by first synthesizing an FPGA implementation. Obviously, 
fast simulators or FPGA support is required when booting full operating 
systems.

 * [Using the Spike Simulator]({{< relref "spike.md" >}})
 * [Using the C++ emulator generated by Chisel]({{< relref "emulator.md" >}})
 * [Simulating the Verilog (ASIC target) generated by Chisel]({{< relref "verilog-asic-sim.md" >}})
 * [Simulating the Verilog (FPGA target) generated by Chisel]({{< relref "verilog-fpga-sim.md" >}})