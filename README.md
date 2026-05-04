# FLUX Hardware Backends

Hardware-accelerated constraint enforcement backends for the FLUX constraint system. Three-tier architecture: **CPU → GPU → ARM**.

## Backends

| Backend | Language | Description |
|---------|----------|-------------|
| **CUDA** | C++/PTX | 5 CUDA kernels + differential tests + benchmarks |
| **CPU** | C/ASM | AVX-512 batch, JIT, retro benchmarks, Fortran kernel |
| **Fortran** | Fortran 90 | `flux_constraint_kernel.f90` — reference constraint kernel |
| **FPGA** | SystemVerilog | `flux_checker_top.sv`, `flux_rau_interlock.sv`, `hdc_judge.v` |
| **eBPF** | C | `flux_ebpf_constraint.c` + `flux_ebpf_loader.c` — kernel-space enforcement |
| **WebGPU** | WGSL/JS | WGSL shader + JS module + test HTML |
| **Vulkan** | GLSL | Vulkan compute shader for constraint evaluation |
| **Coq** | Coq | `flux_p2.v`, `semantic_gap_theorem.v`, `flux_vm_correctness.v` |
| **Formal** | SymbiYosys | Formal verification of RTL |
| **ASM** | Python | `flux_asm.py` — constraint assembler |

## Crates

| Crate | Description |
|-------|-------------|
| `constraint-theory-core-cuda/` | CUDA constraint theory core (Rust + CUDA) |
| `flux-cuda/` | CUDA FLUX crate (C + CUDA) |
| `sonar-vision-c/` | C sonar vision module |
| `flux-isa-c/` | C ISA bindings for FLUX instruction set |

## Benchmarks

| Tier | Throughput |
|------|-----------|
| CPU (single-thread) | 22.3B constraints/s |
| GPU (CUDA) | 1.02B constraints/s |
| CPU (multi-threaded) | 70.1B constraints/s |
| FPGA (LUT usage) | 1,717 LUTs |

## Build

```bash
# CUDA kernels
cd cuda/ && make

# CPU AVX-512
cd cpu/ && make

# FPGA (requires Verilator or synthesis tool)
cd rtl/ && make sim

# eBPF (requires clang + bpftool)
cd ebpf/ && make

# Docker (full build environment)
docker build -t flux-hardware .
```

## License

Apache License 2.0 — see [LICENSE](LICENSE).
