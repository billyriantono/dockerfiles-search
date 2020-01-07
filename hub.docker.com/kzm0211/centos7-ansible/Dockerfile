FROM centos:7

LABEL maintainer=inamuu

RUN yum -y update \
    && \
    yum -y install \
    epel-release \
    ansible \
    vim \
    git \
    python \
    ;\
    yum clean all

RUN curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py \
    && \
    python get-pip.py \
    && \
    rm -f get-pip.py

RUN pip install \
    ansible-lint \
    yamllint

CMD ["/bin/bash"]