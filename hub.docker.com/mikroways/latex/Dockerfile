FROM leoditommaso/latex:1.0.0

MAINTAINER Leandro Di Tommaso <leandro.ditommaso@mikroways.net>

COPY ./pgf.tgz /tmp/
RUN mkdir /root/texmf && \ 
    tar -xvzf /tmp/pgf.tgz -C /root/texmf/ && \
    rm /tmp/pgf.tgz
