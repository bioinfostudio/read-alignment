# Alignment

You already know that there are a number of competing tools for short
read alignment, each with its own set of strengths, weaknesses, and
caveats. Here we will use BWA, a widely used aligner based on the
Burrows-Wheeler Algorithm. The alignment involves two steps- first,
indexing the genome and then running the alignment command. BWA is a
software package for mapping low-divergent sequences against a large
reference genome, such as the human genome. It consists of three
algorithms: BWA-backtrack, BWA-SW and BWA-MEM. The first algorithm is
designed for Illumina sequence reads up to 100bp, while the rest two for
longer sequences ranged from 70bp to 1Mbp. BWA-MEM and BWA-SW share
similar features such as long-read support and split alignment, but
BWA-MEM, which is the latest, is generally recommended for high-quality
queries as it is faster and more accurate. BWA-MEM also has better
performance than BWA-backtrack for 70-100bp Illumina reads (ref:bwa
manual).

BWA has a number of parameters in order to perform the alignment. To
view them all type

    bwa <press enter> 

BWA uses an indexed genome for the alignment in order to keep its memory
footprint small. Because of time constraints we will not be running the
indexing command. It is run only once for a version of genome, and the
complete command to index the human genome version hg19 is given below.

You DO NOT need to run this command. This has already been run for you.

      bwa index -p bwa_index/human_g1k_v37 -a bwtsw bwa_index/human_g1k_v37.fasta
      

This command will output 6 files that constitute the index. These files
that have the prefix `human_g1k_v37` are stored in the `bwa_index`
subdirectory. To view if they files have been successfully created type:

We have used the following arguments for the indexing of the genome.

    > **-p**: Prefix of the output database [same as db filename]
    > **-a**: Algorithm for constructing BWT index. This method works with the whole human genome.
    > **ref genome filename**: the last argument is the name of the reference genome file in the fasta format

```bash
$ ls -l bwa_index
```

Now that the genome is indexed we can move on to the actual alignment.
The first argument for `bwa` is the basename of the index for the genome
to be searched; in our case this is `human_g1k_v37.fasta`.

     bwa mem -M -t 1 -R "@RG\tSM:Blood\tID:ERR059356\tLB:lb\tPL:ILLUMINA" bwa_index/human_g1k_v37.fasta SM_Blood_ID_ERR059356.subset_R1.fastq.gz SM_Blood_ID_ERR059356.subset_R2.fastq.gz > SM_Blood.sam


The above command outputs the alignment in SAM format and stores them in
the file `SM_Blood.sam`.

We have used the following arguments for the alignment of the reads.

    > **mem**: fast mode of high quality input such the Illumina
    > **-M**: Flags extra hits as secondary. This is needed for compatibility with other tools downstream.
    > **-t**: Number of threads.
    > **-R**: Complete read group header line.
