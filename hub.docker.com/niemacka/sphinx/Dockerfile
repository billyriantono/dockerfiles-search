FROM alpine:latest

RUN apk update && \
    apk upgrade && \
    apk add python-dev \
      py-pip \
      make \ 
      git \
      gcc \
      libc-dev \
      texlive-full \
      openssh && \
    pip install --upgrade pip && \
    pip install sphinx==1.4.4 \
      sphinx_rtd_theme \
      docutils==0.12 \
      numpy==1.15.4 \
      sphinx-fortran==1.0.1 \
      recommonmark
