# Files Format
## Reference Genome
A reference genome is like a book that records the complete genetic sequence of an organism with nucleotides ATCG.

* `.fa.gz` is a compressed reference genome file, where `fa` stands for FASTA format and `gz` stands for gzip compression.
* `.fa` is an uncompressed reference genome file, decompressed from the `.fa.gz` file.
* `.fa.fai` is the helper index file for the FASTA file.

A reference genome in FASTA format might look like:
>chr1
ACGT...
>chr2
ACGT...
>chrX
ACGT...
Here, each chromosome is stored as one **sequence** entry.

A `fa.fai` file is like the catalog. Each chromosome is a chapter, and the `fa.fai` file can help you find the page (location on the reference genome) for each chapter.

It might look like:
| Sequence | Length | Offset |
|---|---:|---:|
| chr1 | 248956422 | 6 |
| chr2 | 242193529 | 253404903 |
| chr3 | 198295559 | 500657651 |
| chrX | 156040895 | 2875001522 |
| chrM | 16569 | 3031042417 |
* Sequence - - the name/label of the sequence
* Length - - the length of the sequence
* Offset - - byte position where that sequence starts


## Star
aligner - map reads to genome

lookup structure for fast substring matching


FASTQ
raw input data

FASTQ_trimming
removes sequencing adapters and low-quality read parts

BAM (Binary Alignment/Map File)
the output from STAR alignment
reads, chromosome the read belongs to, genomic coordinates, read quality


segmentation.gtf
divides the genome into annotation categories
