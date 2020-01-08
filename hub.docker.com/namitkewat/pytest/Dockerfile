FROM markadams/chromium-xvfb-py3

MAINTAINER Namit Kewat <namitkewat@gmail.com>

RUN apt-get update && apt-get install -y wget vim

RUN echo 'export PATH=/opt/conda/bin:$PATH' > /etc/profile.d/conda.sh && \
    wget --quiet https://repo.continuum.io/miniconda/Miniconda3-4.3.14-Linux-x86_64.sh -O ~/miniconda.sh && \
    /bin/bash ~/miniconda.sh -b -p /opt/conda && \
rm ~/miniconda.sh

ENV PATH /opt/conda/bin:$PATH

ENV DISPLAY :99

RUN /opt/conda/bin/pip install selenium pytest