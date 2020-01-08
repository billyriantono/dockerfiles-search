FROM alpine:latest


# Inspired by :
# * https://github.com/CognitiveScale/alpine-miniconda

# Install glibc and useful packages
RUN echo "@testing http://nl.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories \
    && apk --update add \
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
    && curl "https://raw.githubusercontent.com/sgerrand/alpine-pkg-glibc/master/sgerrand.rsa.pub" -o /etc/apk/keys/sgerrand.rsa.pub \
    && curl -L "https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.23-r3/glibc-2.23-r3.apk" -o glibc.apk \
    && apk add glibc.apk \
    && curl -L "https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.23-r3/glibc-bin-2.23-r3.apk" -o glibc-bin.apk \
    && apk add glibc-bin.apk \
    && /usr/glibc-compat/sbin/ldconfig /lib /usr/glibc/usr/lib \
    && rm -rf glibc*apk /var/cache/apk/*


# Configure environment
# Configure Miniconda
ENV PATH=/opt/conda/bin:$PATH \
  SHELL=/bin/bash \
  LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8 LANGUAGE=en_US.UTF-8 \
  MINICONDA_URL=https://repo.continuum.io/miniconda/Miniconda3-4.2.12-Linux-x86_64.sh \
  MINICONDA_MD5_SUM=d0c7c71cc5659e54ab51f2005a8d96f3


# Install conda and imagehash
RUN cd /tmp && \
    mkdir -p /opt/conda && \
    curl -L $MINICONDA_URL  -o miniconda.sh && \
    echo "$MINICONDA_MD5_SUM  miniconda.sh" | md5sum -c - && \
    /bin/bash miniconda.sh -f -b -p /opt/conda && \
    rm miniconda.sh && \
    /opt/conda/bin/conda install --yes conda==4.2.12 && \
    pip install imagehash


# Configure container startup
WORKDIR /home
ENTRYPOINT ["/sbin/tini", "--"]
CMD [ "/bin/bash" ]
