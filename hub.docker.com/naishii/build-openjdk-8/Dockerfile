FROM ubuntu-debootstrap:12.04
RUN echo "deb-src http://security.ubuntu.com/ubuntu precise-security universe" >> /etc/apt/sources.list
RUN apt-get update && apt-get build-dep -y \
    openjdk-7 \
 && apt-get install -y \
    openjdk-7-jdk \
    mercurial \
 && rm -rf /var/lib/apt/lists/*
ENV LANG C
ENV PATH /usr/lib/jvm/java-7-openjdk-amd64/bin:${PATH}
