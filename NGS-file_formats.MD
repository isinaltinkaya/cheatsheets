## - Coordinate systems


https://www.biostars.org/p/84686/
https://genome-blog.soe.ucsc.edu/blog/2016/12/12/the-ucsc-genome-browser-coordinate-counting-systems/







## - PAF: a Pairwise mApping Format ([Source](https://github.com/lh3/miniasm/blob/master/PAF.md))

Approximate mapping positions between two set of sequences.
TSV

|Col|Type  |Description                               |
|--:|:----:|:-----------------------------------------|
|1  |string|Query sequence name                       |
|2  |int   |Query sequence length                     |
|3  |int   |Query start (0-based; BED-like; closed)   |
|4  |int   |Query end (0-based; BED-like; open)       |
|5  |char  |Relative strand: "+" or "-"               |
|6  |string|Target sequence name                      |
|7  |int   |Target sequence length                    |
|8  |int   |Target start on original strand (0-based) |
|9  |int   |Target end on original strand (0-based)   |
|10 |int   |Number of residue matches                 |
|11 |int   |Alignment block length                    |
|12 |int   |Mapping quality (0-255; 255 for missing)  |

If PAF is generated from an alignment:

|Col|Type|Description|
|--|--|--|
|10 |int   |Number of sequence matches |
|11 |int   |Total number of sequence matches, mismatches, insertions, deletions  |

- If alignment is not available, column 10 and 11 are still required but may be highly inaccurate.

- A PAF file may optionally contain SAM-like typed key-value pairs at the end of
each line.






# VCF/BCF files

## INFO vs FORMAT fields

- INFO is for describing the variation. Appears in the INFO field. `<key>=<data>[,data]`.
- FORMAT is for describing the samples. Values appear under individual names and multiple fields for each sample are separated by semicolons.
