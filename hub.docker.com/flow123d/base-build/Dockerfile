FROM flow123d/base
MAINTAINER Jan Hybs
ENV LANG C.UTF-8

# Build-time metadata as defined at http://label-schema.org
ARG BUILD_DATE
ARG VCS_REF
ARG VERSION=1.0
ARG BUILD_TYPE=Debug

LABEL org.label-schema.build-date="$BUILD_DATE" \
      org.label-schema.name="Flow123d" \
      org.label-schema.description="Transport Processes in Fractured Media" \
      org.label-schema.url="http://flow123d.github.io/" \
      org.label-schema.vcs-ref="$VCS_REF" \
      org.label-schema.vcs-url="https://github.com/flow123d/flow123d" \
      org.label-schema.vendor="Technical University of Liberec" \
      org.label-schema.version="$VERSION" \
      org.label-schema.schema-version="1.0"

# install various tools and libs
# at the end remove apt files to make images smaller
RUN apt-get update && apt-get install -y \
    cmake \
    git \
    python3-dev \
    python3-pip \
    valgrind \
    perl \
    gfortran \
    gcc \
    g++ \
    pandoc \
    clang \
    vim \
    ccache \
    build-essential \
    libssl-dev \
    libffi-dev \
    libboost-program-options-dev \
    libboost-serialization-dev \
    libboost-regex-dev \
    libboost-filesystem-dev \
    libblas* \
    liblapack* \
    lib32z1 \
    lib32z1-dev \
    libpugixml1v5 \
    libpugixml-dev \
    libpython3.4 \
    oprofile \
 && pip3 install \
    pyyaml \
    loguru \
    markdown \
    psutil \
    simplejson \
    formic \
    pymongo \
    pandoc-fignos \
    pandoc-tablenos \
    cpp-coveralls \
 && apt-get install -y --no-install-recommends  \
    doxygen \
    graphviz \
    texlive \
    texlive-base \
    texlive-binaries \
    texlive-extra-utils \
    texlive-font-utils \
    texlive-fonts-extra \
    texlive-fonts-recommended \
    texlive-generic-recommended \
    texlive-latex-base \
    texlive-latex-extra \
    texlive-latex-recommended \
    texlive-pictures \
    texlive-pstricks \
    texlive-science \
    imagemagick \
    texlive-base \
    lmodern \
 && rm -rf /var/lib/apt/lists/*
 
# save the image version
RUN echo "base-build" > /.dockerversion
