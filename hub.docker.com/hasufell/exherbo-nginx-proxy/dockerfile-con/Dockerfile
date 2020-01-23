FROM golang:1.11.2

# make Apt non-interactive
RUN echo 'APT::Get::Assume-Yes "true";' > /etc/apt/apt.conf.d/90ci \
  && echo 'DPkg::Options "--force-confnew";' >> /etc/apt/apt.conf.d/90ci

ENV DEBIAN_FRONTEND=noninteractive

# man directory is missing in some base images
# https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=863199
RUN apt-get update \
  && mkdir -p /usr/share/man/man1 \
  && apt-get install -y \
    git ca-certificates tar gzip unzip zip bzip2 gnupg curl wget openssh-client gcc make curl \
    libaio1 # required for oracle instantclient

# Installing Oracle Instant Client
RUN curl -L https://bitbucket.org/HasanOzgan/docker-golang-oracle/raw/bfefe65e393918aa28687874c45fc280ae8b431c/instantclient-basic-11.2.zip -o instantclient-basic-11.2.zip
RUN curl -L https://bitbucket.org/HasanOzgan/docker-golang-oracle/raw/bfefe65e393918aa28687874c45fc280ae8b431c/instantclient-sdk-11.2.tgz -o instantclient-sdk-11.2.tgz

RUN unzip -o instantclient-basic-11.2.zip && \
    tar -xvzf instantclient-sdk-11.2.tgz && \
    mv instantclient_11_2/ /usr/lib/ && \
    rm instantclient-basic-11.2.zip instantclient-sdk-11.2.tgz && \
    ln /usr/lib/instantclient_11_2/libclntsh.so.11.1 /usr/lib/libclntsh.so && \
    ln /usr/lib/instantclient_11_2/libocci.so.11.1 /usr/lib/libocci.so && \
    ln /usr/lib/instantclient_11_2/libociei.so /usr/lib/libociei.so && \
    ln /usr/lib/instantclient_11_2/libnnz11.so /usr/lib/libnnz11.so

ENV ORACLE_BASE /usr/lib/instantclient_11_2
ENV LD_LIBRARY_PATH /usr/lib/instantclient_11_2
ENV TNS_ADMIN /usr/lib/instantclient_11_2
ENV ORACLE_HOME /usr/lib/instantclient_11_2

# Setup Oracle Instant for PkgConfig
COPY oci8.pc /usr/local/lib/pkgconfig/oci8.pc

ENV GOPATH /go
WORKDIR /go/src/app

## Oracle Client
RUN go get -u gopkg.in/rana/ora.v4
RUN go get -u github.com/golang/dep/cmd/dep
RUN go get github.com/onsi/ginkgo/ginkgo