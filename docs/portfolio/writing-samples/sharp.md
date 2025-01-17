---
tags:
  - Writing sample
---

# Validating SHARP configuration

## Introduction

NVIDIA Scalable Hierarchical Aggregation and Reduction Protocol (SHARP) reduces the amount of network traffic data between aggregation nodes. Enabling SHARP frees up hardware resources for computation and reduce collective operations time.

This guide describes the methods for validating SHARP configuration on a cluster and/or node. Validating SHARP configuration requries verifying aggregation trees, compute node end-to-end functionality, and running the provided performance benchmarks. 

This guide assumes basic knowledge of high-performance computing systems and Linux command line proficiency.

### Prerequsites

You need the following packages installed:

 * ssh
 * pdsh
 * environment-modules.x86_64

And have either:

* NVIDIA Unified Fabric Manager 

	or

* A dedicated server running Subnet Manager (SM) or openSM

!!! note
    If using a dedicated server, disable the onboard Subnet Manager in your managed switches. Prior to validating your SHARP configuration, make sure your environment meets the setup requirements.

## Validating SHARP

### Verifying aggregation trees

To verify aggregation nodes and tree construction: 

1. In your terminal, run `ibdiagnet --sharp` to access the aggregation trees diagnostics.

2. Identify the number of aggregation nodes located in the **fabric summary** table.

3. Check for errors in the SHARP diagnostics stage by referring to the **fabric summary** table.

4. Use `grep` to count the number of configured aggreations trees in the SHARP diagnostics output file, located in `/var/tmp/ibdiagnet2/ibdiagnet2.sharp` by default. For example:

```bash
$ cat /var/tmp/ibdiagnet2/ibdiagnet2.sharp | grep -c TreeID 126
```

The Aggregation Manager is properly constructing aggregation trees if the number of trees in the output matches the amount configured.  

!!! note
    If operating in dynamic trees mode, ignore `ibdiagnet` warnings regarding multiple distinct trees with the same ID.

### Testing node-to-node functionality

The `sharp_hello` utility tests the end-to-end functionality on compute nodes by creating a single job and sending a barrier request tot he SHARP aggregation node.

The flags for `sharp_hello` are:

```bash
usage:  sharp_hello <-d | --ib_dev> <device> [OPTIONS]
OPTIONS:
    	[-d | --ib_dev]  	- HCA to use
    	[-v | --verbose] 	- libsharp coll verbosity level(default:2)
                              	Levels: (0-fatal 1-err 2-warn 3-info
                                                     4-debug 5-trace)
    	[-V | --version] 	- print program version
    	[-h | --help]    	- show this usage
```

### Using the SHARP benchmark utility

SHARP provides a test script for benchmarking native low-level performance for all_reduce and barrier operations both with and without SHARP. To run the benchmark utility:

From a host running SM and Aggregation Manager:

* Load the HPC-X module and open `sharp_benchmark.sh` to launch the benchmarking script:

```bash
$module load hpcx
$HPCX_SHARP_DIR/sbin/sharp_benchmark.sh
```

!!! warning
    If using NVIDIA SHARP from `MLNX_OFED`, make sure the `HPCX_SHAPR_DIR` environment variable has been redirected to the SHAPR installation directory, located at `/opt/mellanox/sharp` by default. Next, verify the `OMPI_HOME` environment variable is set to the MPI installation directory.

The flags for `sharp_benchmark.sh` are:

```bash
Usage: sharp_benchmark.sh [-t] [-d] [-h] [-f]
    	-t - tests list (e.g. sharp:barrier)
    	-d - dry run
    	-h - display this help and exit
    	-f - suppress error in prerequisites checking
```
