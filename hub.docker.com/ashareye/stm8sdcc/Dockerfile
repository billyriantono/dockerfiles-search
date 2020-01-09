FROM frolvlad/alpine-glibc:latest
LABEL maintainer "ashareye@aliyun.com"

COPY alpine.mirror /etc/apk/repositories
COPY stsw-stm8069.zip /tmp/stsw-stm8069.zip
COPY STM8S_StdPeriph_Lib_sdcc.patch /opt/STM8S_StdPeriph_Lib_sdcc.patch
COPY stsw-stm8016.zip /tmp/stsw-stm8016.zip
COPY STM8L15x-16x-05x-AL31-L_StdPeriph_Lib_sdcc.patch /opt/STM8L15x-16x-05x-AL31-L_StdPeriph_Lib_sdcc.patch
COPY stx-btree-0.9.tar.bz2 /tmp/stx-btree-0.9.tar.bz2
COPY sdcc-src-3.6.0.tar.bz2 /tmp/sdcc-src-3.6.0.tar.bz2

RUN apk --update --no-cache upgrade && \
    apk --update --no-cache add make boost && \
    apk --update --no-cache add --virtual build-dependencies \
    build-base flex bison boost-dev texinfo unzip openssl ca-certificates && \

    unzip /tmp/stsw-stm8069.zip -d /opt && \
    rm -fr /tmp/stsw-stm8069.zip && \
    cd /opt/STM8S_StdPeriph_Lib && \
    patch -p1 <../STM8S_StdPeriph_Lib_sdcc.patch && \
    rm -fr /opt/STM8S_StdPeriph_Lib_sdcc.patch && \
    mv /opt/STM8S_StdPeriph_Lib /opt/STM8SSPL && \

    unzip /tmp/stsw-stm8016.zip -d /opt && \
    rm -fr /tmp/stsw-stm8016.zip && \
    cd /opt/STM8L15x-16x-05x-AL31-L_StdPeriph_Lib && \
    patch -p1 <../STM8L15x-16x-05x-AL31-L_StdPeriph_Lib_sdcc.patch && \
    rm -fr /opt/STM8L15x-16x-05x-AL31-L_StdPeriph_Lib_sdcc.patch && \
    mv /opt/STM8L15x-16x-05x-AL31-L_StdPeriph_Lib /opt/STM8LSPL && \

    tar xvf /tmp/stx-btree-0.9.tar.bz2 -C /tmp && \
    rm -fr /tmp/stx-btree-0.9.tar.bz2 && \
    cd /tmp/stx-btree-0.9 && \
    ./configure && \
    make -j && \
    make install-strip && \
    rm -fr /tmp/stx-btree-0.9 && \

    tar xvf /tmp/sdcc-src-3.6.0.tar.bz2 -C /tmp && \
    rm -fr /tmp/sdcc-src-3.6.0.tar.bz2 && \
    cd /tmp/sdcc-3.6.0 && \
    ./configure \
      --disable-mcs51-port \
      --disable-z80-port \
      --disable-z180-port \
      --disable-r2k-port \
      --disable-r3ka-port \
      --disable-gbz80-port \
      --disable-tlcs90-port \
      --disable-ds390-port \
      --disable-ds400-port \
      --disable-pic14-port \
      --disable-pic16-port \
      --disable-hc08-port \
      --disable-s08-port && \
    make -j && \
    make install && \
    rm -fr /tmp/sdcc-3.6.0 && \

    apk del build-dependencies
