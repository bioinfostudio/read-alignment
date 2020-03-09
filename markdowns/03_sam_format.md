# SAM format

The SAM (Sequence Alignment/Map) format is currently the de facto
standard for storing large nucleotide sequence alignments. It is a
TAB-delimited text format consisting of a header section, which is
optional, and an alignment section. If present, the header must be prior
to the alignments. Header lines start with `@`, while alignment lines do
not. Each alignment line has 11 mandatory fields for essential alignment
information such as mapping position.

Look at the top 10 lines of the SAM file by typing:

```bash
alignment$ head -n 10 SM_Blood.sam
```

Can you distinguish between the header of the SAM format and the actual
alignments?

The header line starts with the letter ‘@’, i.e.:

```
@SQ     SN:GL000192.1   LN:547496
@RG     SM:Blood        ID:ERR059356.subset     LB:lb   PL:ILLUMINA
@PG     ID:bwa  PN:bwa  VN:0.7.15-r1140 CL:bwa mem -M -t 4 -R @RG\tSM:Blood\tID:ERR059356.subset\tLB:lb\tPL:ILLUMINA bwa_index/human_g1k_v37.fasta SM_Blood_ID_ERR059356.subset_R1.fastq.gz SM_Blood_ID_ERR059356.subset_R2.fastq.gz
```

While, the actual alignments start with read id, i.e.:

```
HWI-ST478_0133:3:1101:1496:2034#0       83      3       161091090       60      28S75M  =       161090895       -270    TGCGCACTCGTTCTCTTTTGTCTTCCCCCGACACACCTTGCAATATTGGCAGGGTAGATATGACCACTCAGGGCATGTAGATCAGGAAATAGAAACCCTAAGA ########################C9ADF@DFCA>>=.=EDDE9FFHHFHHHHFFHHEHEEHFGGBDFHHGFEGGGEHHGHGFHFHHHHFHHHHEHHHHHHHH NM:i:0  MD:Z:75 AS:i:75 XS:i:19 RG:Z:ERR059356.subset
HWI-ST478_0133:3:1101:1496:2034#0       163     3       161090895       60      97M6S   =       161091090       270     CAGAGGAAGCTAAAGGTAGATGGGGGCAGGGAAGGGAACCAATAGAAACAGAGCACCTGCTTGGGCCCGTGTTAGCCATTTTACGTAGTTATCATTTTTTTTT HHHHGHGHHHHHGFHGCGGE6EEEEFBFFGHEHHHHEHDHFH:HHBEFABGGHHBHHG?GCBDDFDEEB9A:=>A;?:>?EE0DE;A?6@AE########### NM:i:0  MD:Z:97 AS:i:97 XS:i:21 RG:Z:ERR059356.subset
```


What kind of information does the header provide?

- @SQ: Reference sequence information; SN: reference sequence name; LN: reference sequence length.
- @RG: Read group; ID: Read group identifier; SM: Sample; LB: Library; PL: Platform.
- @PG: Program; ID: Program record identifier; PN: Program name; VN: Program version; CL: the command line that produces the alignment.
