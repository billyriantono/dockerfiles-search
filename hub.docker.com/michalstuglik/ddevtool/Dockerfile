FROM ubuntu:14.04

MAINTAINER Michal Stuglik <stuglik@gmail.com>

RUN apt-get update -y

RUN apt-get install -y wget openssl bzip2 git mercurial subversion

RUN echo 'export PATH=/opt/conda/bin:$PATH' > /etc/profile.d/conda.sh && \
    wget --quiet https://repo.continuum.io/miniconda/Miniconda2-4.0.5-Linux-x86_64.sh && \
    /bin/bash /Miniconda2-4.0.5-Linux-x86_64.sh -b -p /opt/conda && \
    rm Miniconda2-4.0.5-Linux-x86_64.sh && \
    /opt/conda/bin/conda install --yes conda

ENV PATH /opt/conda/bin:$PATH

# http://bugs.python.org/issue19846
# > At the moment, setting "LANG=C" on a Linux system *fundamentally breaks Python 3*, and that's not OK.
ENV LANG C.UTF-8

CMD [ "/bin/bash" ]

RUN conda config --add channels r
RUN conda config --add channels bioconda

# base apps:
RUN conda install -y numpy
RUN conda install -y pysam

