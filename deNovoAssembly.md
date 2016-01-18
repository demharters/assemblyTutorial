# *De-novo* assembly of nanopore reads

This document introduces a typical workflow for the de-novo assembly of Nanopore reads. Due to the unique characteristics of Nanopore reads and continued improvements in chemistry and software, new strategies for assembly are being developed continuously. Here, we will briefly describe one particular workflow that is based on a recently released package called Canu; a de-novo assembler specific for long noisy reads (Canu is derived from the Celera assembler).

```
Several steps are required for the de-novo assembly of raw-sequencing data. Thus, an assembler may be regarded as a collection of modules that takes in a large number of raw sequencing reads and puts out a single consensus sequence.
```

