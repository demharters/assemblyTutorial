# Data Formats
Once the sequencing run has finished, Metrichor will have returned all reads as individual **fast5** files; fast5 is based on [HDF5](http://www.hdfgroup.org/HDF5/)(http://www.hdfgroup.org/HDF5/), adapted by Oxford Nanopore, that contains the basecalled 1D and 2D (if used) sequences as well as supplementary information such as (start and end indices of template/complement strands, median current levels in pA, number of events, quality scores etc.). For assembly we are only interested in the sequences (and possibly the quality scores). The most common formats for storing sequence and sequence with quality scores are **fasta** and **fastq**, respectively. An example of how to convert fast5 into these formats is included in the [alignment exercise](https://github.com/demharters/assemblyTutorial/blob/master/alignment.md).

##### Formats used in this tutorial:
- fast5: Oxford Nanopore’s own version of the HDF5 format (hierarchical data format) used to store nanopore data.
- FASTA: Header + Sequence
- FASTQ: Header + Sequence + Quality score
- SAM (Sequence Alignment/Map format): Header + Alignment
- BAM: binary, compressed SAM data

### FAST5

#### Analysis workflow
The MinION device collects raw data at a sampling frequency in the kHz range (top). MinKNOW performs a non-linear filtering of these data to provide a secondary data stream of events (bottom). All subsequent analysis is performed on these events. The event sequence is available in the .fast5 file (at present the raw data are not provided by default, although Oxford Nanopore Technologies may enable this option in the future).

MinKNOW groups events into reads by detecting the abrupt signal change when DNA enters and leaves the nanopore. Each read is written to an individual .fast5 file and these per-read .fast5 files are passed to Metrichor. The read detection algorithm excludes boundary events, corresponding to the period in which the DNA is not fully threaded into the pore.

#### Fast5 files contain the following information and more:

Event parameter | Description
--- |--- 
mean | mean of raw samples which compose event (in pA)
start | start time of event (in s)
stdv | standard deviation of raw samples which compose event (in pA)
length (time) | length (in s)
model_state | k-mer to which the event has been associated
move | number of bases moved from previous event
weights | a value from zero to one indicating how confident the basecaller is that the event is not a spurious or false positive event
p_model_state | posterior marginal, the probability that model_state gave rise to the observation of the event, given the entire event sequence
mp_model_state | the most probable model state, i.e. the k-mer corresponding to the maximal posterior marginal for this event
p_mp_model_state | posterior marginal, the probability that mp_model_state gave rise to the observation of the event, given the entire event sequence
p_A | probability that this event may be associated with the base A
p_C | probability that this event may be associated with the base C
p_G | probability that this event may be associated with the base G
p_T | probability that this event may be associated with the base T
stay_prob | The probability of the current event being another observation of the same state as the previous event.
step_prob | The probability of the current event being one of the four states that can immediately follow the state of the last event.
skip_prob | The probability of the current event being some other state than those associated with the stay or step probabilities.

#### Segmentation
For 1D basecalling, the leader section is followed by the template DNA, without a hairpin or the complement strand. In order to properly basecall the event data, we first have to segment the event data into these various sections. At the same time we can compute various metrics about these sections which can be used for diagnostic/debug purposes, and which may be important as inputs to the basecalling software component.
