# Manipulate SAM output

SAM files are rather big and when dealing with a high volume of NGS
data, storage space can become an issue. As we have already seen, we can
convert SAM to BAM files (their binary equivalent that are not human
readable) that occupy much less space.

Convert SAM to BAM using `samtools view` and store the output in the
file `SM_Blood.bam`. You have to instruct `samtools view` that the input
is in SAM format (`-S`), the output should be in BAM format (`-b`) and
that you want the output to be stored in the file specified by the `-o`
option:

```bash
$ samtools view -bSo SM_Blood.bam SM_Blood.sam
```

Compute summary stats for the Flag values associated with the alignments
using:

```bash
$ samtools flagstat SM_Blood.bam
```


## Post Alignment Visualisation option

IGV is a stand-alone genome browser that can be used to visualise the
BAM outputs. Please check their [website](http://www.broadinstitute.org/igv/)
for all the formats that IGV can display.

It requires the index of the BAM file to be in the same
folder as where the BAM file is. The index file should have the same
name as the BAM file and the suffix `.bai`. Finally, to create the index
of a BAM file you need to make sure that the file is sorted according to
chromosomal coordinates.

Sort alignments according to chromosomal position and store the result
in the file with the prefix `Blood.sorted`:

```bash
$ samtools sort SM_Blood.bam SM_Blood.sorted
```

Index the sorted file.

```bash
$ samtools index SM_Blood.sorted.bam
```

The indexing will create a file called `Blood.sorted.bam.bai`. Note that
you don’t have to specify the name of the index file when running
`samtools index`, it simply appends a `.bai` suffix to the input BAM
file.
