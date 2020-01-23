FROM ubuntu:latest
MAINTAINER Dimitrij Dugan <dimitrijdugan@gmail.com>

RUN  apt-get -qq update && apt-get -qq -y install curl git \
     && useradd -m fastai \
     && cd /home/fastai

WORKDIR /home/fastai/

USER fastai

RUN curl -sSL https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh -o /home/fastai/miniconda.sh \
    && chmod +x miniconda.sh \
    && mkdir ./.conda \
    && touch ./.conda/environments.txt \
    && ./miniconda.sh -bfp /home/fastai/conda/ \
    && rm ./miniconda.sh \
    && ./conda/bin/conda init \
    && export PATH="/home/fastai/conda/bin:$PATH" \
    && conda update -n base -c defaults conda \
    && conda create -n pytorch \
    && conda install --name pytorch -c pytorch pytorch torchvision cpuonly \
    && git clone https://github.com/fastai/course-v3

