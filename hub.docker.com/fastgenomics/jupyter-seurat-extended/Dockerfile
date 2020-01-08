FROM fastgenomics/jupyter-seurat:0.0.6

COPY environment.yml /
RUN cd /tmp/ \
        && conda env update -n base -f /environment.yml \
        && conda clean -afy

COPY install.R /tmp/install.R
RUN Rscript /tmp/install.R
