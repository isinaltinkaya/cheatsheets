# Duplicate Marking Methods 

## Samtools markdup

(I checked the source code at https://github.com/samtools/samtools/blob/5fcc7a4fa822bb216030b6d6803e846f99b7ad41/bam_markdup.c to verify.)

* Old version was named as "samtools rmdup"

* It works with both single end and paired end sequencing data. 

* Excluded reads (by default): Secondary, supplementary, unmapped, QC failed, reads with read length bigger than 300 bases.

* If the read is soft clipped, it calculates 5’ unclipped start position and uses it.

POS corresponds to the position of first CIGAR “consuming reference”. Soft clipping does not consume reference. Therefore if we have soft clipping at the beginning of the read, the POS is the position after soft clipping.

[Source](https://github.com/samtools/hts-specs/blob/master/SAMv1.pdf)

* They use a hashing method. In the hash they keep chromosome id, unclipped 5’ start position and orientation of the read.

If we use the option `-d` to give optical distance threshold, it uses this threshold to check the differences between x coordinates and y coordinates. 
For example: If we use -d 850; for this example
Read01 x=100 y=200
Read02 x=900 y=1000
It will check x1-x2 AND y1-y2; they are smaller than or equal to our threshold it will mark them as optical duplicates using DT tag. In this case x1-x2=800 < 850 ,y1-y2=800 < 850. Note that it requires both xdiff and ydiff to be <= our threshold. These reads are optical duplicates to each other.

* It does not take inter-tile duplicates into account. It does the comparisons within each tile (tile+swath combination).

* Outputs estimated library size. Does not output a histogram (preseq format).


* How it handles the paired end reads

Creates a hash of the current read and its pair
Uses the unclipped start (or end based on orientation), reference id, orientation and whether the current read is leftmost of the pair
Requires users to use `samtools fixmate -m` first. Markdup uses the tags fixmate sets: MC (mate cigar) and MS (mate score) to decide which read to mark as duplicate. Keeps the read with the highest score as “original”


## Picardtools MarkDuplicates

* Works with SE and PE.

* It takes clipping and gaps into account.

* If we give a coordinate sorted input file, the unmapped mates, secondary and supplementary reads will be excluded and will not be marked as duplicates. But if we give a read query sorted file, they will be included! This is important, we will get different number of duplicates based on sorting of given file.

* It takes into account clipping on the 5′ end of the read and makes calculations based on where the 5′ start position would be if the entire read had mapped to the reference.

* Its comparison is not as complicated as in EstimateLibraryComplexity. It only uses 5’ coordinates and mapping orientation. (I checked the source code at https://github.com/broadinstitute/picard/blob/959411f3a97e979c406cc068ca9200ff4e2bf6bf/src/main/java/picard/sam/markduplicates/MarkDuplicates.java#L962) 

* Picard also uses xdiff and ydiff to compare with optical distance threshold instead of euclidean distance (I checked the source code at https://github.com/broadinstitute/picard/blob/959411f3a97e979c406cc068ca9200ff4e2bf6bf/src/main/java/picard/sam/markduplicates/util/OpticalDuplicateFinder.java#L328). It requires the reads to have the same tile (4 digit integer made of surface+swath+tile information); which means it doesn’t take intertile duplicates into account.

* It identifies the “representative read” using quality score.
