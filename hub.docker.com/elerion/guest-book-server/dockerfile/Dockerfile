FROM frolvlad/alpine-oraclejdk8:cleaned 
RUN apk add --update autoconf automake libtool build-base bash ca-certificates openssl && rm -rf /var/cache/apk/* && update-ca-certificates
WORKDIR /root
RUN wget https://github.com/google/protobuf/releases/download/v2.5.0/protobuf-2.5.0.tar.gz && tar zvxf protobuf-2.5.0.tar.gz && rm protobuf-2.5.0.tar.gz
WORKDIR /root/protobuf-2.5.0
RUN ./autogen.sh
RUN ./configure
RUN make
RUN make install
WORKDIR /root
RUN wget http://xenia.sote.hu/ftp/mirrors/www.apache.org/maven/maven-3/3.3.9/binaries/apache-maven-3.3.9-bin.tar.gz -O maven.tar.gz && tar xvzf maven.tar.gz && rm maven.tar.gz && mv apache-maven* maven
ENV PATH /root/maven/bin:$PATH

