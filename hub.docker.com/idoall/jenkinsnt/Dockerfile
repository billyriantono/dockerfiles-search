FROM centos:6

# Dependencies from https://git-scm.com/book/en/v1/Getting-Started-Installing-Git#Installing-from-Source
RUN yum install -y \
      curl-devel expat-devel gettext-devel openssl-devel zlib-devel make gcc perl-ExtUtils-MakeMaker \
  && yum remove -y git \
  && yum clean all

ENV VERSION=1.7.1
ENV TGZ=https://github.com/git/git/archive/v${VERSION}.tar.gz

# curl -L follows redirects
RUN curl -L -o source.tgz ${TGZ} && \
    tar -xzvf source.tgz && \
    rm source.tgz && \
    cd /git-${VERSION} && \
    make prefix=/usr/local all && \
    make prefix=/usr/local install && \
    rm -rf /git-${VERSION} && \
    git --version
