FROM nextflow/nextflow:0.28.0

ENV SINGULARITY_VERSION=2.5.1

RUN apk update \
    && apk add --update --no-cache \
        curl file build-base autoconf automake libtool linux-headers \
        tar gzip bash python squashfs-tools libarchive-dev libstdc++ \
    && cd /tmp \
    && curl -fSsL https://github.com/singularityware/singularity/releases/download/${SINGULARITY_VERSION}/singularity-${SINGULARITY_VERSION}.tar.gz | tar -zxvpf - \
    && cd singularity-${SINGULARITY_VERSION} \
    && ./configure --prefix=/opt/singularity --sysconfdir=/opt/singularity/etc --localstatedir=/var/lib \
    && make -j4 \
    && make install \
    && cd .. \
    && rm -rf singularity-${SINGULARITY_VERSION} \
    && ldconfig /opt/singularity/lib/singularity \
    && ln -s /opt/singularity/bin/singularity /usr/bin/singularity 
RUN wget https://raw.githubusercontent.com/Zhuvikin/md5deep-alpine/master/hashdeep > /usr/local/bin/hashdeep \
    && chmod +x /usr/local/bin/hashdeep
RUN apk del --purge \
        curl file build-base autoconf automake libtool linux-headers

RUN sed -i "s:bind path = /etc/localtime:#&:" /opt/singularity/etc/singularity/singularity.conf