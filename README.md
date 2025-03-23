
# Notes

An improved version of the cloud-tracking algorithm, which will be a general-purpose fluid volume tracking algorithm, is currently being developed. Given the circumstances, though, it does not appear that I will be writing a paper on the algorithm.

If one wants to use this version of the cloud-tracking algorithm, please cite [Oh and Austin (2014)](https://doi.org/10.1175/JAS-D-24-0018.1):

Oh, G., & Austin, P. H. (2024). Direct Entrainment as a Measure of Dilution. *Journal of the Atmospheric Sciences*, 81(10), 1783-1797.

# Updated cloud-tracking algorithm for SAM #
To run the cloud-tracking algorithm, use 

    python run_tracker.py [Input_dir]

where [Input_dir] is the address of the input directory. The model parameters will automatically be retrieved from the given files. 

## Current Status ##
The cloud-tracking requires Python 3.5.

### Main ###
- [x] Make run_tracker.py run with command arg
- [x] Get rid of config.cfg 
- [x] Read model parameters from xray dataset
- [x] Write model parameters to HDF5 dataset

### Generate cloudlets ###
- [x] Implement/benchmark asyncio operations on ~ 30,000 cloudlet computations
- [x] Numba/Cython for the expansion algorithm (cloudtracker.utility_functions)
- [x] Wrap up with dask -> HDF5 output

### Cluster cloudlets ###
- [x] Filter noisy cloudlets out for speedup
- [x] Threaded HDF5 file read for speed

### Output cloud data ###
- [ ] Wrap file I/O with dask 

## Profiling ##
To profile the cloud-tracking algorithm using line_profiler, do
    
    python -O -B -m kernprof -l -v run_tracker.py > line_stats.txt

or, to run with a memory profiler instead,  

    python -O -B -m memory_profiler run_tracker.py > memory_stats.txt
