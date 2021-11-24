####

### - sort bed file by first chr then coordinate
```
sort -k1,1 -k2,2n $BED_FILE >${BED_FILE}_sorted.bed
```

### - remove "Chr" prefix
```
samtools reheader -c 'perl -pe "s/^(@SQ.*)(\tSN:)Chr/\$1\$2/"' in.bam
```

### - add "chr" prefix
```
samtools reheader -c 'perl -pe "s/^(@SQ.*)(\tSN:)(\d+|X|Y|MT)(\s|\$)/\$1chr\$2\$3/"' in.bam
```
