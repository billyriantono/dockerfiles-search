# Dockerfile based on jupyter/all-spark-notebook.
# See: https://github.com/jupyter/docker-stacks/tree/master/all-spark-notebook

# NOTE:
# Docker currently has a limitation whereby one can't `chown` directories copied into a
# container at build time under certain conditions. This dockerfile copies a directory at
# (on)build time and as a result of the above limitation, it's not possible to change its owner
# from `root` to `jovyan`. That means that when users try to create a notebook inside that
# directory, they will see a `permission denied` error. There is an
# [issue](https://github.com/moby/moby/pull/28499) in github to adress this problem.
# Until then, this image should only be used for local environments with mounted volumes, a
# situation where this problem doesn't occur.

FROM jupyter/all-spark-notebook

MAINTAINER Luis Freire

USER root

# Install all OS dependencies for openai gym
RUN apt-get update && apt-get install -yq --no-install-recommends \
    python-numpy \
    python-dev \
    cmake \
    zlib1g-dev \
    libjpeg-dev \
    xvfb \
    libav-tools \
    xorg-dev \
    python-opengl \
    libboost-all-dev \
    libsdl2-dev \
    swig \
    && apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Install ffmpeg for video handling
RUN echo "deb http://ftp.uk.debian.org/debian jessie-backports main" >> /etc/apt/sources.list && \
    apt-get update && \
    apt-get install -yq --no-install-recommends ffmpeg

# Copy content of project directory and assign ownnership
ONBUILD COPY . /home/$NB_USER/work/

# Add channels to conda to install custom packages
RUN conda config --add channels menpo       # for opencv

# Set the working directory
WORKDIR /home/$NB_USER/work

# Install binary packages with conda from requirements-conda.txt.
# Remove pyqt and qt pulled in for matplotlib since we're only ever going to
# use notebook-friendly backends in these images
ONBUILD RUN conda install --quiet --yes --file requirements-conda.txt && \
            conda remove --quiet --yes --force qt pyqt && \
            conda clean -tipsy

# Install python packages with pip from requirements-pip.txt
ONBUILD RUN pip install --no-cache-dir -r requirements-pip.txt

# Switch back to jovyan to avoid accidental container runs as root
USER $NB_USER
