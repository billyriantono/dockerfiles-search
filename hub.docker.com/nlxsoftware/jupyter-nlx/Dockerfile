# Copyright (c) NLX Software BV
ARG BASE_CONTAINER=jupyter/scipy-notebook
FROM $BASE_CONTAINER

LABEL maintainer="NLX <info@nlx.nl>"

# Install sftp python module
RUN pip install pysftp

USER root

# Install java kernel
RUN conda install --quiet --yes 'openjdk=11.*'
RUN wget -q -O - "https://api.github.com/repos/SpencerPark/IJava/releases/latest" | grep "browser_download_url" | cut -d '"' -f 4 | wget -nv -i - &&\
    mkdir ij && cd ij && unzip ../ijava* && \
    python3 install.py --sys-prefix && \
    cd .. && rm -r ij && rm ijava*

# Prepare migrator folder
COPY start-migrator.sh /usr/local/bin/

CMD ["start-migrator.sh"]
