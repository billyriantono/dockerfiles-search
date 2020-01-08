FROM ubuntu:14.04

RUN apt-get update -qq && \
    apt-get install -y software-properties-common && \
    add-apt-repository ppa:redhawksdr/omnievents-2.7 && \
    add-apt-repository ppa:git-core/ppa && \
    apt-get update -qq && \
    apt-get install -y ant \
                       autoconf \
                       automake \
                       autotools-dev \
                       build-essential \
                       curl \
                       gettext \
                       gfortran \
                       junit4 \
                       libboost-dev \
                       libboost-filesystem-dev \
                       libboost-iostreams-dev \
                       libboost-regex-dev \
                       libboost-system-dev \
                       libboost-thread-dev \
                       libcppunit-dev \
                       libcos4-dev \
                       libcurl4-openssl-dev \
                       liblapack-dev \
                       liblog4cxx10-dev \
                       liboctave-dev \
                       libomnievents-dev \
                       libomniorb4-dev \
                       libopenblas-dev \
                       libnuma-dev \
                       libtool \
                       libxml2-utils \
                       omnievents \
                       omniidl \
                       omniidl-python \
                       omniorb \
                       omniorb-idl \
                       openjdk-7-jdk \
                       python2.7-dev \
                       python-omniorb \
                       python-numpy \
                       python-pip \
                       uuid-dev \
                       uuid-runtime \
                       valgrind \
                       xsdcxx && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN pip install jinja2 \
                nose \
                scipy \
                unittest-xml-reporting

ENV JAVA_HOME /usr/lib/jvm/java-7-openjdk-amd64

ENV GIT_VERSION=2.8.2
RUN curl -fsSL https://www.kernel.org/pub/software/scm/git/git-$GIT_VERSION.tar.gz | tar xzf - -C /usr/src && \
    cd /usr/src/git-$GIT_VERSION && \
    make prefix=/usr/local all && \
    make prefix=/usr/local install && \
    rm -rf /usr/src/git-$GIT_VERSION

COPY omniORB.cfg /etc/

CMD ["/bin/bash", "-l"]
