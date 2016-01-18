# Genome assembly by alignment/mapping to a reference

In this exercise we introduce a simple pipeline for the alignment of Nanopore sequencing data to a known reference sequence. It is by no means a comprehensive guide but should be viewed as a resource for first time users.
Important aspects such as quality control of the initial dataset and the usage of quality scores in the alignment are not covered. 

Software requirements:
- poretools (Toolkit for working with Nanopore data)
- LAST (Alignment software for long reads)
- samtools (A suite of programs for interacting with HT sequencing data)
- Tablet (Alignment/Assembly Viewer)

File formats:
- fast5: Oxford Nanopore’s own version of the HDF5 format (hierarchical data format) used to store nanopore data.
- FASTA: Header + Sequence
- FASTQ: Header + Sequence + Quality score
- SAM (Sequence Alignment/Map format): Header + Alignment
- BAM: binary, compressed SAM data

##### Step 1: Extract 2D reads as FASTQ
Metrichor returns each of the basecalled reads as individual fast5 files. Use poretools to extract the 2D reads from the fast5 folder and store them in a single fasta file with the following command:

```
poretools fasta --type 2D fast5/ > 2Dreads.fasta
```

Note, that we could also have used the fastq format which includes the quality scores and may help with the alignment step. However, for simplicity we will use the fasta format.

##### Step 2: Generate index files
Create the index files required for sequence comparison and alignment by running the following command:

```
lastdb -Q 0 reference.lastindex reference.fasta
-Q	input format: 0=fasta, 1=fastq
```

This will generate a set of files with different extensions (.ssp, .tis, .sds, .des, .prj, .suf, .bck).

##### Step 3: Alignment
Align the extracted 2d reads to the reference sequence with the following command (Nick Loman suggested the parameters, which work quite well):

```
lastal -s 2 -T 0 -Q 0 -a 1 reference.lastindex 2Dreads.fasta > 2Dreads_aligned.maf
-s	0=reverse, 1=forward, 2=both
-T	type of alignment: 0=local, 1=overlap
-Q	input format: 0=fasta, 1=fastq
-a	gap penalty
```

##### Step 4: Generate Genome Viewer friendly alignment
Convert your alignment to the .sam format with maf-convert.py (part of the LAST package):

```
maf-convert sam 2Dreads_aligned.maf > 2Dreads.sam
```

Index your reference file:

```
samtools faidx reference.fasta
```

Compress .sam to .bam:

```
samtools view -b -S -t reference.fasta.fai -o 2Dreads.bam 2Dreads.sam
-b	output BAM
-S	input SAM
-t	reference index file
-o	output file name
```

Sort your alignment by genome location to allow for pile-up:

```
samtools sort 2Dreads_aligned.bam 2Dreads_aligned.sorted
```

Index the sorted to alignment (required to view the alignment in tablet)
```
samtools index 2Dreads_aligned.sorted.bam
```

##### Step 5: Alignment Visualisation

- Open the tablet alignment viewer.
- Go to >Open Assembly.
- Select your sorted alignment file.
- Select your reference.
- In the left column under contigs select your alignment.
- You should now be able to see your assembly.
- To see the coverage, go to > Advanced > Coverage.


