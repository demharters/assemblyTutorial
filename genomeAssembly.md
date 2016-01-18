# Genome Assembly

Advancement in DNA sequencing technologies in recent years have allowed for the rapid and relatively cost effective characterization
of whole genomes. This has opened the door for a variety of applications in areas such as evolutionary biology, medical research,
metagenomics and molecular biology.

In order to make a given genome accessible for DNA sequencing the genetic material is processed to generate a library of shorter
fragments that can be analysed by the sequencer. During this step, however, positional information of the fragments is lost.
Thus, an essential step in whole-genome sequencing (WGS) is to assemble the sequenced fragments (also called reads) back into
their original order as accurately as possible.

There are two main strategies for assembly: 1) map the reads to a reference sequence or 2) assemble the reads de novo, i.e. without a template. Both approaches have their strengths and weaknesses.

Mapping is relatively fast but inherently biases the consensus towards the target sequence. De novo assembly is computationally expensive but is more suitable when it comes to detecting new structural variations. Thus, both methods are often used in a complementary fashion.

```Structural variations include inversions, translocations as well as copy number variations (CNVs), i.e. >1kb deletions and
insertions.```

## Assembly by mapping/alignment
Mapping, also referred to as the alignment of reads against a reference sequence, is commonly used in re-sequencing.  As the name suggests, the reads are mapped one by one to an existing reference sequence. As the number of aligned sequences grows, reads will start to overlap and form contiguous stretches of genomic sequence. Thus, by aligning more and more reads to the reference a stacked set of overlapping sequences is built up, commonly referred to as a pile-up. Depending on the coverage and read accuracy we can then calculate the consensus sequence with a certain confidence. Given that the confidence is high enough we may compare the consensus against the reference to detect genetic variations such as insertions, deletions and SNPs.

```The coverage tells us how many times on average a single base has been covered by a read; defined as LN/G, where L is the read length, N is the number of reads and G is the size of the reference sequence.```

Some of the challenges of mapping/alignment:
- Reads do not include position information, thus we need to find the correct region in the reference sequence.
- Choosing a suitable cutoff for mismatch penalties. Make it too high and we would never see any variation. Make it too low and our alignments would be wrong. 
- Filter out sequencing errors. Allow for a low level of sequencing errors in our reads, and filter them out later.
- Repeat procedure for each read.
