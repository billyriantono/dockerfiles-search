from jupyter/datascience-notebook

RUN conda update -n base conda
RUN conda install -c bioconda bioconductor-biocinstaller bioconductor-metagenomeseq bioconductor-phyloseq bioconductor-deseq2 bioconductor-biomformat bioconductor-genomeinfodbdata=1.2.0 bioconductor-genomeinfodb=1.18.1 bioconductor-iranges bioconductor-dada2 r-ggpubr r-devtools tar r-doparallel bioconductor-msa tar
RUN conda install -c bioconda r-rcurl openssl=1.0
RUN echo 'Sys.setenv(TAR = "/bin/tar"); devtools::install_github("gavinsimpson/ggvegan")' | R --no-save
RUN conda clean --all
