FROM alpine:3.4

MAINTAINER Eemil Väisänen <eemil.vaisanen@iki.fi>

ENV CONDA_PATH /opt/conda
ENV PATH $CONDA_PATH/bin:$PATH
ENV INSTALLER Miniconda3-4.1.11-Linux-x86_64.sh

RUN apk add --upgrade --no-cache libssl1.0 wget ca-certificates \
    && echo "@testing http://nl.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories \
    && apk add --no-cache \
        bash \
        bzip2 \
        unzip \
        sudo \
        libstdc++ \
        glib \
        libxext \
        libxrender \
        tini@testing \
    && cd /tmp \
    && mkdir -p $CONDA_PATH \
    && wget "https://raw.githubusercontent.com/sgerrand/alpine-pkg-glibc/master/sgerrand.rsa.pub" -O /etc/apk/keys/sgerrand.rsa.pub \
    && wget "https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.23-r3/glibc-2.23-r3.apk" -O glibc.apk \
    && wget "https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.23-r3/glibc-bin-2.23-r3.apk" -O glibc-bin.apk \
    && apk add --no-cache glibc.apk glibc-bin.apk \
    && /usr/glibc-compat/sbin/ldconfig /lib /usr/glibc/usr/lib \
    && wget https://repo.continuum.io/miniconda/$INSTALLER \
    && /bin/bash $INSTALLER -f -b -p $CONDA_PATH \
    && rm $INSTALLER \
    && conda update -y conda

ENTRYPOINT ["/sbin/tini", "--"]
CMD [ "/bin/bash" ]
