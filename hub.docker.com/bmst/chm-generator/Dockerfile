FROM ubuntu:18.04

RUN apt update -y && \
    DEBIAN_FRONTEND=noninteractive apt install -y fpc asciidoc && \
    apt clean -y

CMD cd /src && \
    mkdir /tmp/out && \
    a2x -f htmlhelp --destination-dir=/tmp/out index.adoc && \
    cd /tmp/out && \
    chmcmd index.hhp && \
    cp index.chm /out

