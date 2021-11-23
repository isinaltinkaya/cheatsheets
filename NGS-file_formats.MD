## PAF: a Pairwise mApping Format ([Source](https://github.com/lh3/miniasm/blob/master/PAF.md))

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
