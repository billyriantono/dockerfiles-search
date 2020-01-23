FROM bioconductor/devel_core2

RUN sudo apt-get update -y && sudo apt-get install libmagick++-dev -y \
&& R -e 'BiocManager::install(ask = F)' && R -e 'BiocManager::install(c("magick", \
"tidyverse", "devtools", "wesanderson", "ggpmisc", "ggseqlogo", \
"hexbin", "pheatmap", "RColorBrewer", "ComplexHeatmap", "circlize", "gtools","Rsubread", \
"NOISeq", "edgeR", "DESeq2", "derfinder", "derfinderPlot", "regionReport", \
"EDASeq", "RUVSeq", "sva","rafalib", "org.Hs.eg.db", "TxDb.Hsapiens.UCSC.hg38.knownGene",\
"kableExtra", "gridExtra", "clusterProfiler", "gProfileR", "statmod", \
"ggbio", "vqv/ggbiplot", "recount", "plyranges", "rbamtools", ask = F))' && R -e 'tinytex::install_tinytex()'
