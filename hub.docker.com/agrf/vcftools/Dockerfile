FROM agrf/biocontainers_base:4.7.12

# METADATA
ARG VCFTOOLS_VERSION=0.1.16

# ENV
ENV PATH=/opt/conda/bin:$PATH

# INSTALLATION
RUN conda install --channel bioconda --yes --freeze-installed \
    vcftools=${VCFTOOLS_VERSION}

# Clean up image afterwards
RUN conda clean --all --force-pkgs-dirs --yes