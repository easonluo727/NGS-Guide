# General Files Format
## Reference Genome & FASTA
A reference genome is like a book that records the complete genetic sequence of an organism with nucleotides A, T, C, and G.

* `.fa.gz` is a compressed reference genome file, where `fa` stands for FASTA format and `gz` stands for gzip compression.
* `.fa` is an uncompressed reference genome file, decompressed from the `.fa.gz` file.
* `.fa.fai` is the helper index file for the FASTA file.

A reference genome in FASTA format might look like:
```text
>chr1
ACGT...
>chr2
ACGT...
>chrX
ACGT...
```

Here, each chromosome is stored as one **sequence** entry.

A `fa.fai` file is like the catalog. Each chromosome is a chapter, and the `.fa.fai` file helps software quickly jump to where each chromosome sequence starts inside the FASTA file.

A simplified `.fa.fai` file might look like:
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

## Gene Annotation & GTF
GTF stands for **Gene Transfer Format**. It tells you information about the reference genome. It can tell you where a gene starts, where each exon is, which transcript an exon belongs to, and which strand the gene is on. 

A GTF file might look like:
```text
chr1    source    exon    1000    1200    .    +    .    gene_id "GENE1"; transcript_id "TX1";
```

## BED
A BED file records genomic locations. It does not contain the sequencing reads themselves. Tools such as `bedtools` use it to compare genomic regions.
| Chromosome | Start Position | End Position |
|---|---:|---:|
| chr1 | 48,271 | 48,278 |
| chr2 | 63,900 | 63,904 |
| chr3 | 17,544 | 17,536 |
| chrX | 82,116 | 82,119 |
| chrM | 35,687 | 35,692 |


## Reads & FASTQ
Reads are raw input data from the sequencing machine, typically stored in FASTQ format. To effectively analyze the reads, sequencing adapters and low-quality read parts must be removed, or trimmed. Adaptors are helpers to sequencing, but they are not biological sequence.

Files with `fq.gz` are raw reads. Similarly, `fq` stands for FASTQ, and `gz` stands for gzip, which means compressed.


## SAM & BAM
**Sequence Alignment/Map** & **Binary Alignment/Map File**
SAM is human-readable, and BAM is the compressed version for SAM for computer processing, as computer uses a binary system. They contain the same information and play the same role in sequencing. SAM/BAM can be generated from STAR, an aligner that maps reads to genome. SAM and BAM files contain information about reads, chromosome the read belongs to, genomic coordinates, and alignment quality.

A SAM file might look like:
| QNAME | FLAG | RNAME | POS (Start) | End Position* | MAPQ | CIGAR | RNEXT | PNEXT | TLEN | SEQ | QUAL | Optional Tags |
|---|---:|---|---:|---:|---:|---|---|---:|---:|---|---|---|
| SIMREAD001/1 | 99 | chr2 | 48,271 | 48,278 | 60 | 8M | = | 48,321 | 58 | ACTGCCAA | IIIIIIII | `NM:i:0 AS:i:16` |
| SIMREAD001/2 | 147 | chr2 | 48,321 | 48,328 | 60 | 8M | = | 48,271 | -58 | TTGCAACC | IIIIIIII | `NM:i:0 AS:i:16` |
| SIMREAD002 | 0 | chr7 | 63,900 | 63,906 | 42 | 3M1I4M | * | 0 | 0 | AACGTGCA | IIIIIIII | `NM:i:1 AS:i:11` |

Some important columns and their meanings:
`QNAME`     read name / label
`FLAG`      whether the reads are paired
`RNAME`     chromosome the reads align with
`POS`       start position
`MAPQ`      mapping quality, how confident the machine is about the alignment
`CIGAR`     how the reads aligns to the reference, M means alignment match or mismatch
`SEQ`       the read's nucleotide sequence

`.bam.bai` is the index file for a BAM file. Similar to `.fa` and `.fa.fai`, `.bam.bai` is the helper index for `.bam`. It helps software quickly access alignments from a specific genomic region.


## Quick Summary
* FASTA is a file format, reference genome is typically in FASTA
* FASTQ is also a file format, raw sequencing data (sequenced reads) is typically in FASTQ
* STAR is a tool/program, not a file

