# Genome assembly tutorial

```
This tutorial is aimed at researchers with little background in bioinformatics who would like
to start learning about genome assembly. Basic knowledge of the Linux command line is required
(for an introduction see http://linuxcommand.org).
```

In whole genome sequencing (WGS) researchers are usually interested in the original genomic sequence of their sample. However, due to fragmentation of the genome during the preparation of the DNA sequencing library the order of the individual fragments is lost. Thus, the sequenced fragments (reads) need to be correctly stitched back together into their original configuration, a process called genome assembly.

This tutorial explains the two main approaches to genome assembly: 1) The alignment (or mapping) of reads to a reference sequence and 2) the reconstruction of the genomic sequence without a reference (de-novo assembly).

##### Example
A researcher observes a known bacterial strain with an unusual phenotype. He/she would like to sequence the genome to identify the responsible genetic change. Genome assembly using reference alignment would allow for the identification of small alterations in the sequence such as single nucleotide polymorphisms (SNPs), insertions or deletions. However, larger alterations such as duplication events that are not in our reference sequence would be lost. A better approach for detecting these kinds of new structural variations is de-novo assembly. This method requires no prior knowledge of the original sequence but instead attempts to reconstruct the genome from the reads only. Both alignment and assembly have their pros and cons and they often go hand-in-hand during genome analysis.

##### Objectives:
Provide ..
   - a basic understanding of genome assembly
   - a workflow for assembly by alignment 
   - a workflow for de-novo assembly

### Tutorial structure
1. [Introduction](https://github.com/demharters/assemblyTutorial/blob/master/genomeAssembly.md)
2. [Assembly by alignment - workflow example](https://github.com/demharters/assemblyTutorial/blob/master/alignment.md)
3. [*De-novo* assembly - workflow example](https://github.com/demharters/assemblyTutorial/blob/master/deNovoAssembly.md)

If you haven't got your own data you may use this [dataset](https://figshare.com/s/727c9aa81fc4073127d6) and this  [reference](https://figshare.com/s/f524cd2db2c1097726f3) sequence.

##### Further reading:
- [De novo genome assembly versus mapping to a reference genome](beat.wolf.home.hefr.ch/documents/prague.pdf)
- [Beginner’s guide to comparative bacterial genome analysis using next-generation sequence data.](http://microbialinformaticsj.biomedcentral.com/articles/10.1186/2042-5783-3-2)
- Great tutorial on next-gen sequencing genome analysis using [samtools](http://biobits.org/samtools_primer.html) (also covers SNP detection).
- [Celera (Canu) Assembler Terminology](http://wgs-assembler.sourceforge.net/wiki/index.php/Celera_Assembler_Terminology) (some of it is irrelevant to nanoporer reads e.g. mate-pairs).
- [How to score genome assemblies](https://code.google.com/p/ngopt/wiki/How_To_Score_Genome_Assemblies_with_Mauve) with [Mauve](http://darlinglab.org/mauve/mauve.html)
- [QUAST: quality assessment tool for genome assemblies](http://bioinformatics.oxfordjournals.org/content/29/8/1072.abstract)
- Some presentations on genome analysis by the [Schatz lab](http://schatzlab.cshl.edu/teaching/).
