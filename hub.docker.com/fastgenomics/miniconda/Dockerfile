FROM alpine:3.7

# add additional mirror
RUN echo http://mirror1.hs-esslingen.de/pub/Mirrors/alpine/v3.7/main >> /etc/apk/repositories; \
    echo http://mirror1.hs-esslingen.de/pub/Mirrors/alpine/v3.7/community >> /etc/apk/repositories

# based on https://hub.docker.com/r/c12e/alpine-miniconda/~/dockerfile/
RUN apk --update --no-cache add \
    bash \
    git \
    curl \
    ca-certificates \
    bzip2 \
    unzip \
    sudo \
    libstdc++ \
    glib \
    libxext \
    libxrender \
    tini \
    && curl -L "https://github.com/andyshinn/alpine-pkg-glibc/releases/download/2.25-r0/glibc-2.25-r0.apk" -o /tmp/glibc.apk \
    && curl -L "https://github.com/andyshinn/alpine-pkg-glibc/releases/download/2.25-r0/glibc-bin-2.25-r0.apk" -o /tmp/glibc-bin.apk \
    && curl -L "https://github.com/andyshinn/alpine-pkg-glibc/releases/download/2.25-r0/glibc-i18n-2.25-r0.apk" -o /tmp/glibc-i18n.apk \
    && apk add --allow-untrusted /tmp/glibc*.apk \
    && /usr/glibc-compat/sbin/ldconfig /lib /usr/glibc-compat/lib \
    && /usr/glibc-compat/bin/localedef -i en_US -f UTF-8 en_US.UTF-8 \
    && rm -rf /tmp/glibc*apk /var/cache/apk/*

# configure environment
ENV CONDA_DIR=/opt/conda CONDA_VER=4.3.14
ENV PATH=$CONDA_DIR/bin:$PATH SHELL=/bin/bash LANG=C.UTF-8

# install conda
RUN mkdir -p $CONDA_DIR && \
    echo export PATH=$CONDA_DIR/bin:'$PATH' > /etc/profile.d/conda.sh && \
    curl https://repo.continuum.io/miniconda/Miniconda3-${CONDA_VER}-Linux-x86_64.sh  -o mconda.sh && \
    /bin/bash mconda.sh -f -b -p $CONDA_DIR && \
    rm mconda.sh && \
    $CONDA_DIR/bin/conda install --yes conda==${CONDA_VER}

# install base images
RUN conda create -n fastgenomics -y python=3.6 \
	numpy=1.12.1 \
	pandas=0.20.2 \
	scipy=0.19.1 \
	h5py=2.7.0 \
	pyyaml=3.12 \
	statsmodels=0.6.1
