FROM frolvlad/alpine-glibc:alpine-3.9_glibc-2.28

RUN apk add --update --no-cache unzip libaio

ADD instantclient-basiclite-linux.x64-18.5.0.0.0dbru.tar.bz2 /opt
ADD instantclient-sqlplus-linux.x64-18.5.0.0.0dbru.tar.bz2 /opt
ADD instantclient-tools-linux.x64-18.5.0.0.0dbru.tar.bz2 /opt

WORKDIR /opt

ENV ORACLE_HOME /opt/instantclient_18_5
ENV LD_LIBRARY_PATH "/opt/instantclient_18_5"
ENV PATH "$PATH:/opt/instantclient_18_5"

ENTRYPOINT ["sqlplus"]
CMD ["--help"]
