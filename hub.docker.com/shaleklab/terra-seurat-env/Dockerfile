FROM us.gcr.io/broad-dsp-gcr-public/terra-jupyter-bioconductor:0.0.2

RUN R -e "install.packages(c('corpcor', 'ClusterR', 'irlba', 'uwot'))" && \
	R -e 'install.packages("fitdistrplus")' && \
	R -e "BiocManager::install('lfa')" && \
	R -e "BiocManager::install('qvalue')" && \
	R -e 'install.packages("hdf5r")' && \
	R -e "devtools::install_version(package = 'Seurat', version = package_version('3.1.0'))" && \ 
	R -e "devtools::install_github('ncchung/jackstraw')" && \
	R -e "devtools::install_github(repo = 'ChristophH/sctransform')" && \
	R -e "devtools::install_github(repo = 'mojaveazure/loomR', ref = 'develop')" && \
	R -e 'install.packages("VennDiagram")' && \
	R -e 'install.packages("igraph")'

## Install python packages needed for a few Bioc packages
RUN python3 -m pip install --upgrade pip \
    && python3 -m pip install scanpy umap-learn firecloud
