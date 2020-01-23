FROM continuumio/miniconda
MAINTAINER Maximiliano Osorio <mosorio@inf.utfsm.cl>

ARG BUILD_DATE
ARG VCS_REF
LABEL org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.name="Internal-Extinction" \
      org.label-schema.description="The int_ext workflow (Filgueira et al., 2015) calculates the internal extinction factor of galaxies. Using the galaxy catalog provided by AMIGA" \
      org.label-schema.url="https://github.com/rosafilgueira/dispel4py_workflows" \
      org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.vcs-url="https://github.com/dockerpedia/internal_extinction" \
      org.label-schema.vendor="DockerPedia" \
      org.label-schema.version="1.0" \
      org.label-schema.schema-version="1.0" \
      org.label-schema.docker.cmd="docker run -ti --name internal-extinction dockerpedia/internal_extinction:latest bash"

RUN apt-get update \
    && apt-get install -y wget \
        curl \
        python-setuptools \
        git \
        openmpi-bin \
        openmpi-common \
        libopenmpi-dev

ADD internal.yaml /tmp/internal_extinction.yaml
RUN conda env update -f /tmp/internal_extinction.yaml
RUN git clone https://github.com/rosafilgueira/dispel4py_workflows.git