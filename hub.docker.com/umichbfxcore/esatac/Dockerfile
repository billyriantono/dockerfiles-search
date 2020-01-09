FROM bioconductor/release_core2:R3.6.0_Bioc3.9

RUN apt-get -y install \
    libgsl-dev \
    build-essential \
    libssl-dev \
    libssh2-1-dev \
    libcurl4-openssl-dev \
    libsqlite-dev \
    libicu-dev \
    libbz2-dev \
    liblzma-dev \
    libxml2-dev \
    libpcre3-dev \
    texlive \
    pandoc \
    default-jre \
    default-jdk && \
    R CMD javareconf

RUN Rscript -e "\
    install.packages(c(\
        'boot', \
        'devtools', \
        'gplots', \
        'optparse', \
        'tidyverse')); \
    BiocManager::install(c(\
        'annotatr', \
        'BSgenome.Hsapiens.UCSC.hg19', \
        'BSgenome.Hsapiens.UCSC.hg38', \
        'BSgenome.Mmusculus.UCSC.mm10', \
        'chipenrich', \
        'esATAC', \
        'GO.db', \
        'org.Hs.eg.db', \
        'org.Mm.eg.db', \
        'TxDb.Hsapiens.UCSC.hg19.knownGene', \
        'TxDb.Hsapiens.UCSC.hg38.knownGene', \
        'TxDb.Mmusculus.UCSC.mm10.knownGene'), \
    ask = FALSE, update = TRUE);"
