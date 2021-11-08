####

## sort bed file by first chr then coordinate
sort -k1,1 -k2,2n $BED_FILE >${BED_FILE}_sorted.bed
