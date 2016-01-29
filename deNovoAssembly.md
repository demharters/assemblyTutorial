# *De-novo* assembly with nanopore reads

This document introduces a typical workflow for the *de-novo* assembly of Nanopore reads. Due to the unique characteristics of Nanopore reads and continued improvements in chemistry and software, new strategies for assembly are being developed continuously. Here, we will briefly describe one particular workflow that is based on a recently released package called Canu; a *de-novo* assembler specific for long noisy reads (Canu is derived from the Celera assembler).

```
Several steps are required for the de-novo assembly of raw-sequencing data. Thus, a de-novo assembler
may be regarded as a collection of modules that takes in a large number of raw sequencing reads
and puts out a consensus sequence.
```

### *De-novo* assembly with Canu
Canu operates in three main stages: Correction, Trimming and Unitigging.
For each stage an overlapping step is required. The algorithm and parameters may be configured separately for each overlapping step. Currently two **overlapping algorithms** are implemented in Canu:

```
1) MinHash alignment process (MHAP)
MHAP makes use of a probabilistic algorithm to identify overlaps between noisy long reads [1].
Reads are compressed by a dimensionality reducing technique called MinHash [2], which collapses
each sequence into an array of a few integers, called a sketch. The similarity between reads is
estimated by comparing their respective sketches, which can be an order of magnitude smaller
than their sequences. This allows for a significant reduction in dimensionality, thereby
increasing the computational efficiency of the algorithm substantially. MHAP outputs
alignment-free overlaps and is generally suitable for raw uncorrected reads.
```

```
2) Ovl Overlapper
The ovl overlapper is the classic overlapper for Celera Assembler. It may be used in most
scenarios but requires relatively large computational resources. It uses a classic
seed-and-extend algorithm and returns alignments (as opposed to MHAP). This algorithm is
used at the trimming and unitigging stages.
```

##### Stage 1: Correction
Due to the relatively high noise of Nanopore data, error correction is essential to ensure successful *de-novo* assembly. This step has previously been done with hybrid approaches that used accurate short reads to correct the low accuracy long reads. However, it has been shown that a set of long reads with a certain coverage may be sufficient for self-correction [3]. Canu for example identifies a set of target reads and uses overlapping reads from the entire data set for correction. 
In this case MHAP is used as an efficient way to find overlapping reads while the FalconSense algorithm [4] aligns and corrects the reads.

```
For an alternative method for the correction of long noisy reads see www.github.com/jts/nanocorrect/.
```

##### Stage 2: Trimming
Once the reads have been corrected, the reads are cut into shape to remove any low quality sequence from the ends. The trimming stage selects the biggest segment for each corrected read so that the error, overlap and coverage are above selected thresholds.

##### Stage 3: Unitigging
The corrected and trimmed reads are now ready to be stitched back together into their original configuration. A unitigger algorithm finds the best overlap on each end of each read and generates so called unitigs. A unitig contains a high confidence, contiguous, unique sequence up to a boundary that is defined by a branch (i.e. a point of ambiguity) in the overlap graph. Canu deploys the bogart algorithm (best overlap graph) for this purpose.

### Installing and running Canu

Canu can be downloaded [here](https://github.com/marbl/canu).
The Canu documentation can be found [here](http://canu.readthedocs.org/en/latest/index.html).

Software requirements:
	Java SE 8+
	GCC 4.5+

The default command for running canu with nanopore reads is (assuming that you have already extracted your fasta files from the fast5 files using e.g. poretools. See the [alignment tutorial](https://github.com/demharters/assemblyTutorial/blob/master/alignment.md) for details.):

```
canu -p ecoli -d ecoli-oxford genomeSize=4.8m -nanopore-raw oxford.fasta
```

This generates a set of files for each of the three stages (including html reports). Your consensus file will be stored in the current folder.

- For assessing your assembly see e.g. [QUAST](http://bioinf.spbau.ru/quast).
- For annotating your assembly see e.g. [Patric](https://www.patricbrc.org/portal/portal/patric/Home)
