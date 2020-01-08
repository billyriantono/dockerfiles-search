FROM centos:centos7

LABEL maintainer jsuzuki20120311 <shukatu.2012.5.25@gmail.com>

ARG NODE_VERSION=stable
ENV NODE_VERSION ${NODE_VERSION}

RUN yum -y install which && \
    yum -y install perl && \
    curl -L git.io/nodebrew | perl - setup && \
    echo 'export PATH=$HOME/.nodebrew/current/bin:$PATH' >> $HOME/.bashrc && \
    ~/.nodebrew/current/bin/nodebrew install-binary $NODE_VERSION && \
    ~/.nodebrew/current/bin/nodebrew use $NODE_VERSION

ENV PATH $HOME/.nodebrew/current/bin:$PATH

CMD [ "/bin/bash" ]

