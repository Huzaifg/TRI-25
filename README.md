# TRI-25
This is a repository containing all the work I did at my Toyota Research Insititute (TRI) internship with instructions on how to reproduce the work. I worked on implementing a GPU version of the hydroelaastic contact query in [Drake](https://drake.mit.edu/). Here are some features and results
- The query was an overall 10x speedup over the existing CPU version. Certain portions of the contact query, such as the Narrow Phase was close to a 100x faster than the CPU implementation
- The query is written in [SYCL](https://www.khronos.org/sycl/). This allows the query to run on both the CPU and GPU (AMD/Nvidia) without any rewrites.
- The GPU query uses modern GPU friendly data structures and algorithms in the Broad Phase, such as the [Linear-Bounding-Volume-Hierarchy (LBVH)](https://diglib.eg.org/server/api/core/bitstreams/ad092db2-6aec-4f2c-941d-8687de258f00/content). 
- The code works in Drake and works with all Drake simulations consisting of Complaint-Compliant contact. Using this work, and [setting a flag in the multibody plant](https://github.com/Huzaifg/drake/blob/02a0fc390cbee2384f51629fe512a1b52dd46a5a/multibody/plant/multibody_plant.h#L2679), you can get a 10x boost in contact detection.

# Final Presentation
Here is a link to the slides of my final presentation- [Hydroelastic Collision on the GPU](https://docs.google.com/presentation/d/1uyYwbWwe2sZIB1tRxPuLwuwoZeNeU1QD/edit?usp=sharing&ouid=102692614036713066732&rtpof=true&sd=true).

# Reproducing Benchmarks
## Dependencies
The SYCL Proximity Engine requires installing the [Intel OneAPI Base Toolkit](https://www.intel.com/content/www/us/en/developer/tools/oneapi/base-toolkit.html), [Nvidia GPU Drivers and the Nvidia CUDA Toolkit](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html) (tested uptil 12.8) and the Nvidia backend from CodePlay. We recommend following the instructions [here](https://developer.codeplay.com/products/oneapi/nvidia/2025.2.0/guides/get-started-guide-nvidia) for installing all the dependencies. 

## Clutter
The Clutter benchmark exists on branch `convex_integrator_compliant_clutter_sycl` in [Vince's Drake fork](https://github.com/vincekurtz/drake/tree/convex_integrator_compliant_clutter_sycl). Clone the repository and checkout the correct branch.  

Then, to run both the CPU and GPU benchmark, from the repository root, run
```bash
bash clutter_scaling_benchmark.sh
```
To only run the GPU benchmark, run
```bash
bash clutter_scaling_benchmark_gpu.sh
```
To only run the CPU benchmark, run
```bash
bash clutter_scaling_benchmark_cpu.sh
```
## Spatula Scaling
The Spatula scaling benchmark exists on branch `convex_integrator_compliant_clutter_sycl` in [Vince's Drake fork](https://github.com/vincekurtz/drake/tree/convex_integrator_compliant_clutter_sycl). Clone the repository and checkout the correct branch.

Then, to run both the CPU and GPU benchmark, from the repository root, run
```bash
bash spatula_sims.sh
```
To only run the GPU benchmark, run
```bash
bash spatula_sims_gpu.sh
```
To only run the CPU benchmark, run
```bash
bash spatula_sims__cpu.sh
```
## Object Scaling
THe Object scaling benchmark is grippers and peppers falling onto a table. It exists on branch `feature/bvh_broad_phase` in [Huzaifa's Drake fork](https://github.com/Huzaifg/drake/tree/feature/bvh_broad_phase). Clone the repository and checkout the correct branch.


Then, to run both the CPU and GPU benchmark, from the repository root, run
```bash
bash ‎object_scaling_custom_benchmark.sh
```
To only run the GPU benchmark, run
```bash
bash ‎object_scaling_custom_benchmark_gpu.sh
```
To only run the CPU benchmark, run
```bash
bash ‎object_scaling_custom_benchmark_cpu.sh
```
## Barret Hand
The Barret Hand benchmark tests the SYCL Proximity engine on the Barrent hand with both discrete and continuous solvers. It exists on branch `sycl/gears_convex_int` in [Joe's Drake_examples repository](https://github.com/joemasterjohn/drake_examples/tree/sycl/gears_convex_int). Clone the repository and checkout the correct branch.  
Then, install [Vince's Drake fork](https://github.com/vincekurtz/drake/tree/convex_integrator_compliant_clutter_sycl) on the `convex_integrator_compliant_clutter_sycl` branch. Finally, make sure you set the correct `PYTHONPATH`.
```
export PYTHONPATH=<path_to_vince_fork>/build/install/lib/python3.10/site-packages:${PYTHONPATH}
```

Then, from  [Joe's drake_examples repository](https://github.com/joemasterjohn/drake_examples/tree/sycl/gears_convex_int), to run both the CPU and GPU benchmark, run
```bash
bash gear_runs.sh
```
To only run the GPU benchmark, run
```bash
bash gear_runs_gpu.sh
```
To only run the CPU benchmark, run
```bash
bash gear_runs_cpu.sh
```

## Anzu Sim
This benchmark exists on the branch `convex_integrator_experiment_compliant_dishrack_sycl` on [Vince's Anzu fork](https://github.shared-services.aws.tri.global/vincent-kurtz/anzu/tree/convex_integrator_experiment_compliant_dishrack_sycl). Use [Vince's Drake fork](https://github.com/vincekurtz/drake/tree/convex_integrator_compliant_clutter_sycl) as the local drake. To build.......


Then, to run both the CPU and GPU benchmark, from the repository root, run
```bash
bash ‎anzu_sim.sh
```
To only run the GPU benchmark, run
```bash
bash ‎anzu_sim_gpu.sh
```
To only run the CPU benchmark, run
```bash
bash anzu_sim_cpu.sh
```
## Plotting results
All the plotting scripts can be found in [Huzaifa's Drake fork](https://github.com/Huzaifg/drake/tree/feature/bvh_broad_phase) under the [performance_plotting_scripts](https://github.com/Huzaifg/drake/tree/feature/bvh_broad_phase/performance_plotting_scripts) folder.
You can use the utility script [plot_all.sh](https://github.com/Huzaifg/drake/blob/feature/bvh_broad_phase/plot_all.sh) in [Huzaifa's Drake fork](https://github.com/Huzaifg/drake/tree/feature/bvh_broad_phase) to generate all the plots for each of the benchmarks. This script checks for the right data folders in the root of [Huzaifa's Drake fork](https://github.com/Huzaifg/drake/tree/feature/bvh_broad_phase). These data folders need to be manually moved from where the benchmark was run.

# Documentation
Over the course of the internship, I wrote a few docs. Here is a list with links
1) [Profiling SYCL Kernels](https://drive.google.com/file/d/19UMRKk6EqVKKoD1_cJaF4FdWXNs68t76/view?usp=sharing)
2) [Profiling a SYCL Application](https://drive.google.com/file/d/1TrBd0rWDrXwQicLIW2CEecmUoV0fqz0G/view?usp=sharing)
3) [Rough literature review for trees on GPU](https://drive.google.com/file/d/1ytM9sFw8T-cydKTOBILxMYFaMOGs8cma/view?usp=sharing)
4) SYCL Learnings


