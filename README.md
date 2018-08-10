# R_bioinformatics

## Liftover .bed from hg19 to GRCh38
```
# Import the chain file
chain <- rtracklayer::import.chain("/mnt/home/stephen.williams/chain_files/hg19ToHg38.over.chain")

# Do the lyftover and remake the Granges
rpm_48917 = rtracklayer::liftOver(rpm_48917, chain)
rpm_48917 <- unlist(rpm_48917)
rpm_48917 <- as.data.frame(rpm_48917)
```

## Read in .gtf and get some info about a gene
```
mm10_GRCh38_gtf <- rtracklayer::import("/mnt/opt/refdata/GRCh38_and_mm10/genes/genes.gtf")
# get gene cords
mm10_GRCh38_gtf[mm10_GRCh38_gtf@elementMetadata$gene_name == "AGRN" & mm10_GRCh38_gtf@elementMetadata$type == "gene"]

# get the exon cords
mm10_GRCh38_gtf[mm10_GRCh38_gtf@elementMetadata$gene_name == "AGRN" & mm10_GRCh38_gtf@elementMetadata$type == "exon"]
```

## Get exon cords from biomart
```
# GRCh38
gb <- getBM(attributes=c("chromosome_name", "exon_chrom_start","exon_chrom_end"), 
            filters ="ensembl_gene_id", values="ENSG00000012048", 
            mart=useMart(biomart="ensembl", dataset="hsapiens_gene_ensembl"),
            bmHeader=TRUE)
# GRCh37    
gb <- getBM(attributes=c("chromosome_name", "exon_chrom_start","exon_chrom_end"), 
            filters ="ensembl_gene_id", values="ENSG00000012048", 
            mart=useMart(biomart="ensembl", dataset="hsapiens_gene_ensembl", host="grch37.ensembl.org"),
            bmHeader=TRUE)
```
