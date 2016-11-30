# Data Formats
Once the sequencing run has finished, Metrichor will have returned all reads as individual **fast5** files; a **hierarchical data format (HDF5)**, adapted by Oxford Nanopore, that contains the basecalled 1D and 2D sequences as well as supplementary information such as (start and end indices of template/complement strands, median current levels in pA, number of events, quality scores etc.). For assembly we are only interested in the sequences (and possibly the quality scores). The most common formats for storing sequence and sequence with quality scores are **fasta** and **fastq**, respectively. An example of how to convert fast5 into these formats is included in the [alignment exercise](https://github.com/demharters/assemblyTutorial/blob/master/alignment.md).

##### Formats used in this tutorial:
- fast5: Oxford Nanopore’s own version of the HDF5 format (hierarchical data format) used to store nanopore data.
- FASTA: Header + Sequence
- FASTQ: Header + Sequence + Quality score
- SAM (Sequence Alignment/Map format): Header + Alignment
- BAM: binary, compressed SAM data

FAST5

Event parameter | Description
--- |--- 
mean | mean of raw samples which compose event (in pA)
start | start time of event (in s)
stdv | standard deviation of raw samples which compose event (in pA)
length | length (in s) | model_state
k-mer to which the event has been associated
move
number of bases moved from previous event
weights
a value from zero to one indicating how confident the basecaller is that the event is not a spurious or false positive event
p_model_state
posterior marginal, the probability that model_state gave rise to the observation of the event, given the entire event sequence
mp_model_state
the most probable model state, i.e. the k-mer corresponding to the maximal posterior marginal for this event
p_mp_model_state
posterior marginal, the probability that mp_model_state gave rise to the observation of the event, given the entire event sequence
p_A
probability that this event may be associated with the base A
p_C
probability that this event may be associated with the base C
p_G
probability that this event may be associated with the base G
p_T
probability that this event may be associated with the base T
