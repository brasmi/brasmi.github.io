---
tags:
  - Writing sample
---

# Validating SHARP configuration

## Introduction

NVIDIA Scalable Hierarchical Aggregation and Reduction Protocol (SHARP) reduces the amount of network traffic data between aggregation nodes. Enabling SHARP frees up hardware resources for computation and reduce collective operations time.

Verifying SHARP configuration requries validating aggregation trees, compute node end-to-end functionality, and running the provided performance benchmarks.

!!! note
    NVIDIA SHARP requires either NVIDIA Unified Fabric Manager (UFM), or a dedicated server running Subnet Manager (SM) or openSM. If using a dedicated server, disable the onboard Subnet Manager in your managed switches. Prior to validating your SHARP configuration, make sure your environment meets the setup requirements.

## Validating SHARP

### Aggregation trees

1. In your terminal, run `ibdiagnet --sharp` to access the aggregation trees diagnostics.

2. Identify the number of aggregation nodes located in the **fabric summary** table.

3. Check for errors in the SHARP diagnostics stage by referring to the **fabric summary** table.

4. Verify proper construction of trees by Aggregation Manager by using `grep` to analyze the SHARP diagnostics output file, located in `/var/tmp/ibdiagnet2/ibdiagnet2.sharp` by default. For example:

```bash
# Count the number of TreeID instances in the ibdiagnet2 sharp file
$ cat /var/tmp/ibdiagnet2/ibdiagnet2.sharp | grep -c TreeID 126
```

!!! note
    If operating in dynamic trees mode, ignore `ibdiagnet` warnings regarding multiple distinct trees with the same ID.