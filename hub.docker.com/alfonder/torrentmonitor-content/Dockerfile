FROM alpine:3.8

ENV TAURUS_VERSION 1.12.1

RUN apk --update add \
    linux-headers \
    openjdk8 \
    python \
    python-dev \
    py-pip \
    libc-dev \
    libxml2-dev \
    libxslt-dev \
    zlib \
    gcc

RUN pip install --upgrade pip bzt

RUN cd /root/ \
    && wget https://archive.apache.org/dist/jmeter/binaries/apache-jmeter-4.0.tgz \
    && tar -xvzf apache-jmeter-4.0.tgz \
	&& rm -rf apache-jmeter-4.0.tgz \
    && mkdir -p .bzt/jmeter-taurus/ \
    && cp -r apache-jmeter-4.0/ /root/.bzt/jmeter-taurus/4.0 \
	&& rm -rf apache-jmeter-4.0

RUN cd /root/ \
    && wget https://download.microsoft.com/download/2/F/C/2FC75210-EDDE-464C-8E54-45C0291032FF/sqljdbc_7.0.0.0_enu.tar.gz \
    && tar -xf sqljdbc_7.0.0.0_enu.tar.gz \
    && cd sqljdbc_7.0/enu/ \
    && cp mssql-jdbc-7.0.0.jre8.jar /root/.bzt/jmeter-taurus/4.0/lib/ext/mssql-jdbc-7.0.0.jre8.jar

RUN cd /root/ \
    && rm -rf sqljdbc_7.0 \
    && rm -rf sqljdbc_7.0.0.0_enu.tar.gz
