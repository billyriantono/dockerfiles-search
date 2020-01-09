###############################################################################
FROM sfbelaine/common:latex

LABEL maintainer="openscience.elaine@uni-rostock.de"

# Install git
RUN apt update && \
    apt install -y \
        git && \
    apt clean && \
    rm -rf /var/lib/apt/lists/*
