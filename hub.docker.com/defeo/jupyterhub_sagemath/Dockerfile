FROM debian:buster

MAINTAINER Luca De Feo <luca.defeo@polytechnique.edu>

RUN apt-get update -qq && apt-get install -y --no-install-recommends \
        jupyter-notebook \
	python3-pip \
	python3-setuptools \
        sagemath \
	sagemath-jupyter \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

RUN pip3 install jupyterhub==0.8.0

RUN useradd -m sage
ENV HOME=/home/sage
WORKDIR $HOME
USER sage
RUN sage -c

CMD ["jupyterhub-singleuser"]
