FROM fastgenomics/jupyter-base:0.1.9

COPY requirements_conda.txt /tmp/

# Add channles in such order that the highest priority comes last

RUN conda config --add channels bioconda --add channels conda-forge && \
        conda install -q --file /tmp/requirements_conda.txt && \
        conda clean -afy

# because R is R
ENV R_GZIPCMD=/bin/gzip
USER root
RUN ln -s /bin/tar /bin/gtar
USER jovyan


COPY install.R /tmp/install.R
RUN Rscript /tmp/install.R

# run jupyter lab build just to make sure everything is up-to-date after package install
RUN jupyter lab build
