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
