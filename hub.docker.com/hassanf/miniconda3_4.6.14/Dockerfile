FROM centos:7.6.1810
MAINTAINER Hassan Foroughi

RUN yum -y update \
    && yum install -y which wget bzip2 graphviz git gcc fontconfig \
    && wget https://repo.continuum.io/miniconda/Miniconda3-4.6.14-Linux-x86_64.sh -O ~/miniconda.sh \
    && bash ~/miniconda.sh -b -p /usr/local/miniconda \
    && rm -rf ~/miniconda.sh \
    && export PATH="/usr/local/miniconda/bin:${PATH}" \
    && conda clean --all --yes \
    && yum clean all

ENV PATH="/usr/local/miniconda/bin:${PATH}"

ENTRYPOINT ["exec", "$@"]
CMD [ "/bin/bash" ]
