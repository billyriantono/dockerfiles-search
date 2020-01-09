FROM bioconductor/release_core2


RUN apt-get update
RUN apt-get install -y curl wget libboost-all-dev libudunits2-dev gawk

# Install miniconda
RUN wget https://repo.continuum.io/miniconda/Miniconda2-latest-Linux-x86_64.sh
RUN bash Miniconda2-latest-Linux-x86_64.sh -b -p /opt/miniconda2
RUN /opt/miniconda2/bin/conda config --add channels defaults
RUN /opt/miniconda2/bin/conda config --add channels conda-forge
RUN /opt/miniconda2/bin/conda config --add channels bioconda

# Install software required for chipseq pipeline with bioconda
RUN /opt/miniconda2/bin/conda install -c bioconda samtools=1.9 bowtie=1.2.2 macs2=2.1.1.20160309 preseq=2.0.3 \
deeptools=3.1.1 multiqc=1.6a0 samblaster=0.1.24 wiggletools=1.2.2 pysam=0.15.0.1 bedops=2.4.35 r-spp=1.15.2 \
ucsc-bedgraphtobigwig=366 fastqc=0.11.8 picard=2.18.7

# Install fastp manually because bioconda verison is not the latest
RUN wget http://opengene.org/fastp/fastp
RUN chmod a+x ./fastp
RUN mv ./fastp /usr/local/bin

# R packages and bioconductor
RUN R --slave -e "source('https://bioconductor.org/biocLite.R'); \
                    biocLite(c('ChIPseeker', 'org.Mm.eg.db', 'org.Hs.eg.db', 'TxDb.Mmusculus.UCSC.mm9.knownGene', 'TxDb.Mmusculus.UCSC.mm10.knownGene', 'TxDb.Hsapiens.UCSC.hg19.knownGene', 'TxDb.Hsapiens.UCSC.hg18.knownGene'))" 

RUN R --slave -e 'install.packages(c("ggplot2", "data.table", "RColorBrewer", "devtools", "spp"), repos="https://cloud.r-project.org/")'

# Update path
RUN export PATH="/opt/miniconda2/bin:$PATH"
RUN export PATH=/usr/local/bin:$PATH
