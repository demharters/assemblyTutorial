# Data Formats
Once the sequencing run has finished, Metrichor will have returned all reads as individual **fast5** files; a **hierarchical data format (HDF5)**, adapted by Oxford Nanopore, that contains the basecalled 1D and 2D sequences as well as supplementary information such as (start and end indices of template/complement strands, median current levels in pA, number of events, quality scores etc.). For assembly we are only interested in the sequences (and possibly the quality scores). The most common formats for storing sequence and sequence with quality scores are **fasta** and **fastq**, respectively. An example of how to convert fast5 into these formats is included in the [alignment exercise](https://github.com/demharters/assemblyTutorial/blob/master/alignment.md).

##### Formats used in this tutorial:
- fast5: Oxford Nanopore’s own version of the HDF5 format (hierarchical data format) used to store nanopore data.
- FASTA: Header + Sequence
- FASTQ: Header + Sequence + Quality score
- SAM (Sequence Alignment/Map format): Header + Alignment
- BAM: binary, compressed SAM data
