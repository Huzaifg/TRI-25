# TRI-25
Repository containing all the work I did at my TRI internship with instructions on how to reproduce the work.

# Dependencies
The SYCL Proximity Engine requires installing the [Intel OneAPI Base Toolkit](https://www.intel.com/content/www/us/en/developer/tools/oneapi/base-toolkit.html), [Nvidia GPU Drivers and the Nvidia CUDA Toolkit](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html) (tested uptil 12.8) and the Nvidia backend from CodePlay. We recommend following the instructions [here](https://developer.codeplay.com/products/oneapi/nvidia/2025.2.0/guides/get-started-guide-nvidia) for installing all the dependencies. 

# Reproducing Benchmarks
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
The Barret Hand benchmark tests the SYCL Proximity engine on the Barrent hand with both discrete and continuous solvers. It exists on branch `sycl/gears_convex_int` in [Joe's drake_examples repository](https://github.com/joemasterjohn/drake_examples/tree/sycl/gears_convex_int). Clone the repository and checkout the correct branch.  
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
# Plotting results
All the plotting scripts can be found in [Huzaifa's Drake fork](https://github.com/Huzaifg/drake/tree/feature/bvh_broad_phase) under the [performance_plotting_scripts](https://github.com/Huzaifg/drake/tree/feature/bvh_broad_phase/performance_plotting_scripts) folder.
TODO - Add shell script to run all plotting scripts at once


