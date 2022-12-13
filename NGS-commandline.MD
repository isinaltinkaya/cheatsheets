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

### - linearize fasta file then fetch sequences by id
```
#linearize the fasta file 
perl -pe '$. > 1 and /^>/ ? print "\n" : chomp' hla_gen.fasta > hla_gen_linear.fasta

#find the type (ID) and get the type +its next line for each match
while IFS=, read -r id type;do grep -F -A1 --no-group-separator $type hla_gen_linear.fasta > ${id}.fasta ;done < HG00733_MHC_types.csv 
```

### - blast

create blast database
```
ncbi-blast-2.12.0+/bin/makeblastdb -in ${i} -title ${i%.fasta} -dbtype nucl -parse_seqids
```

blast query to database
```
ncbi-blast-2.12.0+/bin/blastn -num_threads 4 -query QUERY.fa -db DATABASE 
```


### - Create a FASTA file with a single contig of N characters

```bash
# Repeat the character 'A' N times and write to a file efficiently using "dd"
dd if=/dev/zero bs=1 count=${N}  | tr '\0' 'A' >  ${OUTPUT_FILE}
# Add a new line at the end of the file, if it is not already there
sed -i -e '$a\' ${OUTPUT_FILE} 
# Append '>CONTIG1' to the beginning of the file
sed -i -e '1s/^/>CONTIG1\n/' ${OUTPUT_FILE}
```


### - Create ANGSD sites file (chr pos major minor) from BCF using REF and first ALT 

```bash
bcftools query -f '%CHROM\t%POS\t%REF\t%ALT{0}\n' ${BCF} > sites.txt
```