#################################################################
# Dockerfile
#
# Software:         BioWardrobe PCA script
# Software Version: v0.0.6
# Description:      Dockerized version of PCA script from BioWardrobe
# Website:          https://github.com/Barski-lab/workflows
# Provides:         PCA script from BioWardrobe
#                   argparse 1.1.1
#                   jsonlite 1.5
#                   scatterplot3d 0.3-41
#                   run_pca.R
# Base Image:       biowardrobe2/scidap-addons:v0.0.6
# Build Cmd:        docker build --rm -t biowardrobe2/pca:v0.0.6 -f pca-Dockerfile .
# Pull Cmd:         docker pull biowardrobe2/pca:v0.0.6
# Run Cmd:          docker run --rm -ti biowardrobe2/pca:v0.0.6
#################################################################
# Argparse, jsonlite, scatterplot3d and FindPython are set to the
# specific versions to garantee that they will work on R 3.2.3-4
# inherited from the base image.
#
# v0.0.6
# Updated run_pca.R script
# - use genelist file to limit input genes
#
# v0.0.5
# Updated run_pca.R script
# - increased marker size
#
# v0.0.4
# Updated run_pca.R script
# - use default value for --combine RefseqId, GeneId, Chrom, TxStart, TxEnd, Strand
#   if not provided
#
# v0.0.3
# Updated run_pca.R script
# - if --name was not provided, set it from --input basenames
#
# v0.0.2
# Updated run_pca.R script
# - to produce images with 800x800 size
# - to save TSV file with the name for the first column
#################################################################


### Base Image
FROM biowardrobe2/scidap-addons:v0.0.6
MAINTAINER Michael Kotliar "misha.kotliar@gmail.com"
ENV DEBIAN_FRONTEND noninteractive


################## BEGIN INSTALLATION ######################

WORKDIR /tmp

ENV VER_ARGPARSE 1.1.1
ENV URL_ARGPARSE "https://github.com/trevorld/argparse/archive/v${VER_ARGPARSE}.tar.gz"

ENV VER_FINDPYTHON 1.0.3
ENV URL_FINDPYTHON "https://github.com/trevorld/findpython/archive/v${VER_FINDPYTHON}.tar.gz"

ENV VER_JSONLITE 1.5
ENV URL_JSONLITE "https://github.com/jeroen/jsonlite/archive/v${VER_JSONLITE}.tar.gz"

ENV VER_SCATTERPLOT3D 0.3-41
ENV URL_SCATTERPLOT3D "https://github.com/cran/scatterplot3d/archive/${VER_SCATTERPLOT3D}.tar.gz"

COPY ./scripts/install_from_source.R /tmp/install_from_source.R
COPY ./scripts/run_pca.R /usr/local/bin/run_pca.R

### Installing dependencies
RUN apt-get update && \
    apt-get install libxml2-dev -y && \

### Installing Argparse and FindPython packages from source
    Rscript /tmp/install_from_source.R "${URL_FINDPYTHON}" && \
    Rscript /tmp/install_from_source.R "${URL_JSONLITE}" && \
    Rscript /tmp/install_from_source.R "${URL_ARGPARSE}" && \
    Rscript /tmp/install_from_source.R "${URL_SCATTERPLOT3D}" && \

### Installing run_pca.R R script
    chmod +x /usr/local/bin/run_pca.R && \

### Cleaning
    apt-get clean && \
    apt-get purge && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/* && \
    strip /usr/local/bin/*; true
