FROM google/cloud-sdk:latest
MAINTAINER tsukasa.tamaru<tsukasa.tamaru@2dfacto.co.jp>

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y openssh-server \
                       sudo \
                       gcc \
                       make \
                       autoconf \
                       libcurl4-gnutls-dev \
                       libexpat1-dev \
                       gettext \
                       libz-dev \
                       libssl-dev \
                       git \
                       expect

# Default to UTF-8 file.encoding
ENV LANG C.UTF-8

RUN echo "deb http://ftp.de.debian.org/debian jessie-backports main" >> /etc/apt/sources.list \
	&& apt-get update \
	&& apt-get install -y openjdk-8-jdk

# see CA_CERTIFICATES_JAVA_VERSION notes above
RUN /var/lib/dpkg/info/ca-certificates-java.postinst configure
RUN update-alternatives --set java /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java

# Install Git
RUN git clone -b v2.6.3 https://github.com/git/git.git /usr/local/src/git
RUN apt-get remove -y git

WORKDIR /usr/local/src/git
RUN make configure && \
    ./configure --prefix=/usr/local && \
    make && \
    make install
WORKDIR /var/jenkins_home

# Setup Jenkins
RUN echo "jenkins ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers
RUN sed -i 's/PermitRootLogin without-password/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd
RUN mkdir -p /var/run/sshd
RUN adduser jenkins
RUN echo "jenkins:jenkins" | chpasswd
RUN echo "export PATH=$PATH:/google-cloud-sdk/bin/" >> /home/jenkins/.bashrc

# Cleanup
RUN apt-get autoclean && \
    apt-get clean && \
    rm -rf /usr/local/src/* && \
    rm -rf /var/lib/apt/lists/*

# Finalize
EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]

