https://docs.ycrc.yale.edu/clusters-at-yale/job-scheduling/


$ ls sim/slurm_logs/logs_231205_152335/smk_simulate_vcfgl_var_qs_error_*err | cut -d_ -f 10|cut -d. -f1 | xargs -I jobid sacct -j jobid --format=JobName,MaxRSS,Elapsed -P --delimiter=,

 for i in sim/slurm_logs/logs_231205_152335/smk_simulate_vcfgl_var_qs_error_*err ;do echo $i|
cut -d_ -f 10|cut -d. -f1 | xargs -I jobid sacct -j jobid --format=JobName,MaxRSS,Elapsed -P --delimiter=,|cut -d, -f2|grep -v "^MaxRSS"|grep  -v "^$"|tr -d "K";done 
https://github.com/CSCfi/slurm-stats/tree/master
