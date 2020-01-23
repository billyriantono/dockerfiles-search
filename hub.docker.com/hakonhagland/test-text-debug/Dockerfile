FROM ubuntu:16.04
LABEL version="1.0" maintainer="Håkon Hægland <hakon.hagland@gmail.com>" perl5version="5.22"

RUN apt-get update \
    && apt-get install -y build-essential curl cpanminus vim
WORKDIR /root
COPY lib lib
COPY t t
COPY xt xt
RUN ls -l
COPY Changes Makefile.PL MANIFEST README ./
RUN cpanm -v .
COPY entrypoint.sh .
ENTRYPOINT ["sh", "-c", "./entrypoint.sh"]
