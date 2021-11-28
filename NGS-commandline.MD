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

### - replace RG
```
samtools addreplacerg -r "ID:XXXX" -o OUT.bam IN.bam
```

### - remove comment lines
```
samtools reheader -c 'grep -v ^@CO' in.bam
```


### - split a vcf file to samples
```
bcftools +split -S <(bcftools query -l ${VCF_FILE}) ${VCF_FILE} -o ${OUTPUT_DIR}
```
