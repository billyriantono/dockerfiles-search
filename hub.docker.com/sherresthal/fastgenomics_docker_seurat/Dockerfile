# Dockerfile how to build fg_r_seurat image

FROM r-base:3.5.3

# libs are needed by devtools and stringr
RUN apt-get update && apt-get install -y \
    build-essential \
    libcurl4-gnutls-dev \
    libxml2-dev \
    libssl-dev \
    libv8-dev \
    pandoc \
    pandoc-citeproc \
    python3-pip

# install our dependencies, Seurat and other R-packages from CRAN
COPY install /install
RUN Rscript /install/install_pkgs.R


# install Python modules (UMAP, Louvain, virtualenv for tensorflow) required by Seurat
RUN pip3 install umap-learn==0.3.7
RUN pip3 install leidenalg==0.7.0
RUN pip3 install virtualenv