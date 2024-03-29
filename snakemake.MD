# snakemake

## Filling up the tmpdir

If you force-cancel a complex job you might fill up the tmpdir quite fast. To avoid this specify a tmpdir location in your bashrc


```
# ~/.bashrc
export TMPDIR='/path/to/mytmpdir'
```

Or also in smk file to make sure a conda env or something like that did not overwrite your TMPDIR env variable

```
# ~/.bashrc
export MYTMPDIR='path/to/mytmpdir'
```


```
# Snakefile
import os
os.environ['TMPDIR'] = os.environ['MYTMPDIR']
```


## etc


https://github.com/snakemake/snakemake/blob/f55801bfabfb916f77fa4ec8f9eb0667e5c8a92e/snakemake/benchmark.py

https://stackoverflow.com/a/66872577/7870777

| col   |   type (unit)   | description                                                                                                                                                                         |
|-----------|:---------------:|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `s`         | float (seconds) | Running time in seconds                                                                                                                                                             |
| `h:m:s`     |    string (-)   | Running time in hour, minutes, seconds format                                                                                                                                       |
| `max_rss`   |    float (MB)   | Maximum "Resident Set Size”, this is the non-swapped physical memory a process has used.                                                                                            |
| `max_vms`   |    float (MB)   | Maximum “Virtual Memory Size”, this is the total amount of virtual memory used by the process                                                                                       |
| `max_uss`   |    float (MB)   | “Unique Set Size”, this is the memory which is unique to a process and which would be freed if the process was terminated right now.                                                |
| `max_pss`   |    float (MB)   | “Proportional Set Size”, is the amount of memory shared with other processes, accounted in a way that the amount is divided evenly between the processes that share it (Linux only) |
| `io_in`     |    float (MB)   | the number of MB read (cumulative).                                                                                                                                                 |
| `io_out`    |    float (MB)   | the number of MB written (cumulative).                                                                                                                                              |
| `mean_load` |    float (-)    | CPU usage over time, divided by the total running time (first row)                                                                                                                  |
| `cpu_time`  |     float(-)    | CPU time summed for user and system                                                                                                                                                 |





## Delete all the outputs up to a certain rule if specified, otherwise only output of first rule by default

snakemake --delete-all-output <rule name>	
