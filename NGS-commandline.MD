####

### - sort bed file

If you have a chr prefix, e.g.
```
chr1 10 20
chr2 10 20
```

use the following command for sorting:
```
sort -V ${file}
```

If you do not have a chr prefix, e.g.

```
1 10 20
2 10 20
```

use the following command for sorting:
```
sort -n -k1 -k2 ${file}
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
