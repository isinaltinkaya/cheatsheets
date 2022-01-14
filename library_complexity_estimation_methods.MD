# Library Complexity Estimation Methods


### Samtools

* SAMtools Library complexity estimation is based on the probability of choosing the same fragment after doing x sampling with replacements (see https://github.com/samtools/samtools/blob/5fcc7a4fa822bb216030b6d6803e846f99b7ad41/bam_markdup.c#L1340, https://github.com/samtools/samtools/blob/5fcc7a4fa822bb216030b6d6803e846f99b7ad41/bam_markdup.c#L1346 )
Here they use Lander-Waterman equation.

```
x=number of unique fragments (truth, we don’t know this)

c=number of observed unique fragments (or read pairs if PE) we calculate after marking duplicates

n=total number of fragments (or read pairs if PE) we have
```

`Coverage = c/x`

While n goes to infinity, the coverage equation is:

`c / x = 1 - exp(-n/x) `

They solve this for x.

`(c/x) -1 + exp(-n/x) = 0`

Here we know `c` and `n`. If we find an `x` value that satisfies this (results with 0 or close to zero), this x value is our estimated library size.

They solve and report this estimated x value as “estimated library size”, which is the number of fragments our library is made of (truth).

If the estimated library size is close to our current library size, the library does not contain more fragments than we have, we wouldn’t observe much new fragments with a new sequencing compared to the current one, thus we shouldn’t sequence it again.


### Picard EstimateLibraryComplexity

* Only uses paired end sequencing data.

* They first sort the reads by the first 5 bases (default) for the first read and second read in pairs. By default (MIN_IDENTICAL_BASES) first 5 bases should be identical for the reads to be further considered as duplicates.

* By default, the mean of base qualities in each read should be at least 20 for the read to be included in the calculations.

* They then compare the sequences in the “possible duplicate groups”, which contains reads that have the same sequence for the first 5 bases of both first and second read in a pair (explained above). They do pairwise comparisons for all reads in the group using MAX_DIFF_RATE threshold, which refers to the maximum rate of differences between two reads to call them identical. They exclude the first 5 bases since we already require them to be identical. Default value if MAX_DIFF_RATE is 0.03. (This happens at https://github.com/broadinstitute/picard/blob/959411f3a97e979c406cc068ca9200ff4e2bf6bf/src/main/java/picard/sam/markduplicates/ElcIdenticalBasesDuplicatesFinder.java )

* It requires minimum 2 (default for MIN_GROUP_COUNT) duplicate groups. For example, if we only observe one unique fragment 100 times, it will give an error and will not calculate library complexity. Another example: If we have 3 unique fragments being observed 40, 20,70 times it means it has 3 groups and the calculation will be made. 

* We can define OPTICAL_DUPLICATE_PIXEL_DISTANCE which is the maximum distance between two duplicate clusters in order to consider them as optical duplicates.
 
* In the manual they note “For the patterned flowcell models, 2500 is more appropriate. For other platforms and models, users should experiment to find what works best. Default value: 100” 

* They report the results for each library. Therefore libraries have distinct calculations. (https://github.com/broadinstitute/picard/blob/959411f3a97e979c406cc068ca9200ff4e2bf6bf/src/main/java/picard/sam/markduplicates/util/LibraryIdGenerator.java)

* They build a histogram in this format:
`#reads in duplicate set -> #of duplicate sets`

[source](https://github.com/broadinstitute/picard/blob/e7cda057968907a9e774b59c320037cfdc6471ad/src/main/java/picard/sam/markduplicates/EstimateLibraryComplexity.java#L562) 

Library complexity estimation: https://github.com/broadinstitute/picard/blob/e7cda057968907a9e774b59c320037cfdc6471ad/src/main/java/picard/sam/DuplicationMetrics.java#L135

* They use the same calculation as samtools markdup (Lander-Waterman equation).

* They then do an effective yield estimation. They calculate ROI (return on investment) we would get if we sequenced the library x higher coverage than the observed coverage. (https://github.com/broadinstitute/picard/blob/e7cda057968907a9e774b59c320037cfdc6471ad/src/main/java/picard/sam/DuplicationMetrics.java#L190 )

* The use the estimated library size to further estimate the ROI at different coverage values.

It does not output a histogram that can be used with preseq.


