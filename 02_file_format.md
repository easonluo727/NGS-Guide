# Files Format
## Reference Genome & FASTA
A reference genome is like a book that records the complete genetic sequence of an organism with nucleotides A, T, C, and G.

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

A `fa.fai` file is like the catalog. Each chromosome is a chapter, and the `.fa.fai` file helps software quickly jump to where each chromosome sequence starts inside the FASTA file.

A simplified FASTA file might look like:
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

## Gene annotation & gtf
GTF stands for **Gene Transfer Format**. It tells you information about the reference genome. It can tell you where a gene starts, where each exon is, which transcript an exon belongs to, and which strand the gene is on. 

A GTF file might look like:
```text
chr1    source    exon    1000    1200    .    +    .    gene_id "GENE1"; transcript_id "TX1";
```

## Reads & FASTQ
Reads are raw input data from the sequencing machine, typically stored in FASTQ format. To effectively analyze the reads, sequencing adapters and low-quality read parts must be removed, or trimmed. Adaptors are helpers to sequencing, but they are not biological sequence.

Files with `fq.gz` are raw reads. Similarly, `fq` stands for FASTQ, and `gz` stands for gzip, which means compressed.


## STAR
**Spliced Transcripts Alignment to a Reference**

It is basically an aligner that maps reads to genome. STAR tells where this read most likely come from, including **chromosome**, **genomic coordinate**, **strand**, and **alignment quality** (how confident it is). To do its job, STAR needs STAR index and FASTQ files. STAR index is a shortcut table that lets STAR quickly find matching positions.

It outputs an alignment file in SAM or BAM format, which will be discussed later.


## SAM & BAM
**Sequence Alignment/Map** & **Binary Alignment/Map File**
SAM is human-readable, and BAM is the compressed version for SAM for computer processing, as computer uses a binary system. They contain the same information and play the same role in sequencing. As mentioned before, SAM/BAM is the output from STAR alignment, containing information about reads, chromosome the read belongs to, genomic coordinates, and alignment quality.

A SAM file might look like:
```text
@HD     VN:1.6     SO:coordinate
@SQ     SN:chr1    LN:248956422
@SQ     SN:chr2    LN:242193529
@PG     ID:STAR    PN:STAR    VN:2.7.10a

read_001    0     chr1    10025    255    50M        *    0    0    ACGTACGTACGT...    FFFFFFFFFFFF...
read_002    16    chr2    30510    255    48M2S      *    0    0    TTGCAAGTCCAA...    FFFFFFFFAAAA...
read_003    0     chr1    50000    255    25M100N25M *    0    0    AGCTTAGCTA...       FFFFFFFFFF...
```

where header lines start with `@`.
If you are interested in what each column means, you may look into it more deeply.


## Quick Summary
* FASTA is a file format, reference genome is typically in FASTA
* FASTQ is also a file format, raw sequencing data (sequenced reads) is typically in FASTQ
* STAR is a tool/program, not a file

