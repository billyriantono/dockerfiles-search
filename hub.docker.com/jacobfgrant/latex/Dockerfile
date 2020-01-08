# LaTeX Dockerfile
FROM ubuntu:18.04

LABEL maintainer="Jacob F. Grant"
LABEL name="latex"

ENV DEBIAN_FRONTEND=noninteractive 

ARG USER_NAME=latex
ARG USER_HOME=/home/latex
ARG USER_ID=1000
ARG USER_GECOS=LaTeX

RUN adduser \
    --home "$USER_HOME" \
    --uid $USER_ID \
    --gecos "$USER_GECOS" \
    --shell /bin/bash \
    --disabled-password \
    "$USER_NAME"

RUN apt-get update && apt-get install -y \
    texlive-base \
    texlive-latex-recommended \
    texlive \
    texlive-latex-extra

RUN apt-get clean -y

WORKDIR "$USER_HOME"

VOLUME [ "$USER_HOME" ]
