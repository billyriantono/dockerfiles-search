FROM centos:6
MAINTAINER 178inaba <178inaba@users.noreply.github.com>

# Install wget, git dependent package.
RUN yum -y update && \
    yum -y install curl-devel expat-devel gcc gettext-devel openssh-clients openssl-devel perl-ExtUtils-MakeMaker wget && \
    yum clean all

# Install git.
ENV GIT_VER 2.10.2
RUN wget https://www.kernel.org/pub/software/scm/git/git-$GIT_VER.tar.gz && \
    tar -zxf git-$GIT_VER.tar.gz && \
    rm -rf git-$GIT_VER.tar.gz && \
    cd git-$GIT_VER && \
    make prefix=/usr/local all && \
    make prefix=/usr/local install && \
    cd .. && \
    rm -rf git-$GIT_VER

# Install golang.
ENV GO_VER 1.7.3
RUN wget https://storage.googleapis.com/golang/go$GO_VER.linux-amd64.tar.gz && \
    tar -C /usr/local -xzf go$GO_VER.linux-amd64.tar.gz && \
    rm -v go$GO_VER.linux-amd64.tar.gz
ENV PATH $PATH:/usr/local/go/bin

# Install supervisor.
RUN wget https://bootstrap.pypa.io/ez_setup.py -O - | python && \
    easy_install supervisor && \
    echo_supervisord_conf > /etc/supervisord.conf
