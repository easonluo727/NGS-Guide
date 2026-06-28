# CLIPseq
Crosslinking Immunoprecipitation followed by Sequencing

## Workflow
1. protein binds to RNA -> protein-RNA complex
2. use an antibody to pull down the protein-RNA complex
3. trim RNA into short fragments and digest the protein (as we only want RNA!)
4. add adaptors, convert RNA to cDNA, PCR amplify, sequence the library



## Environment Manager
- micromamba - environment/package manager - install software
- conda - environment/package manager - install software



## iCount
- use BAM to identify crosslink sites
- use gtf file to identify types of crosslink regions (exon, intron, etc.)



## Samtools
### samtools view
print out alignments in SAM text format
- samtools view -b      - - output as BAM file
- samtools view -q     - - keep only reads with mapping quality higher than 30
- samtools view -c     - - count reads instead of printing them
- samtools view -F 4     - - keep only mapped reads


### samtools index
- create an index file for a BAM (a bam.bai)


### samtools idxstats
- summarize how many reads map to each chromosome
- chromosome name, length, mapped reads, unmapped reads



## DESeq2
test whether each peak different between the two groups

### Input count matrix:
| peak_id | Ctrl2-HS | Ctrl3-HS | PD2-HS | PD3-HS |
|---|---:|---:|---:|---:|
| peak_1 | 96 | 80 | 10 | 12 |
| peak_2 | 4 | 7 | 50 | 55 |
| peak_3 | 0 | 2 | 1 | 3 |

B = PD2-HS, PD3-HS
A = Ctrl2-HS, Ctrl3-HS


### Distribution analysis:
It uses all sample read counts in each group to learn the overall difference between the two groups for each peak.

**log2 FC = log2(reads in B / reads in A)**


### create a DESeqDataSet container
Example:

```r
dds <- DESeqDataSetFromMatrix(
  countData = count_mat,
  colData = coldata,
  design = ~ condition
)
```

use DESeq2 to process the container (pass the container into the function)
Example:

```r
dds <- DESeq(dds)
```


### Extract the result

1. `results(dds, contrast = c("condition", B, A))`
2. `results(dds, name = "condition_B_vs_A")`

### Shrinkage

Shrinkage stabilizes noisy log2 fold-change estimates, especially for low-count features.

1. Normal: `lfcShrink(type = "normal")`
2. apeglm: `lfcShrink(type = "apeglm")`


### Visualization
