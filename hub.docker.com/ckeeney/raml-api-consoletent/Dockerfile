# Copyright (c) cjadeveloper
# Distributed under the terms of the Modified BSD License.

# Based on jupyter/minimal-notebook
# https://hub.docker.com/r/jupyter/minimal-notebook/dockerfile
ARG BASE_CONTAINER=cjadeveloper/jupyter-base
FROM $BASE_CONTAINER

LABEL maintainer="Cristian Javier Azulay <cjadeveloper@gmail.com>"

USER root

# Install all OS dependencies for fully functional notebook server
RUN apt-get update && apt-get install -yq --no-install-recommends \
    build-essential \
    emacs \
    git \
    inkscape \
    jed \
    libsm6 \
    libxext-dev \
    libxrender1 \
    lmodern \
    netcat \
    pandoc \
    python-dev \
    texlive-fonts-extra \
    texlive-fonts-recommended \
    texlive-generic-recommended \
    texlive-latex-base \
    texlive-latex-extra \
    texlive-xetex \
    tzdata \
    unzip \
    nano \
    && rm -rf /var/lib/apt/lists/*

# Switch back to johndoe to avoid accidental container runs as root
USER $NB_UID
