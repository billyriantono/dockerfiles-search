# Dockerfile based on jupyter/all-spark-notebook.
# See: https://github.com/jupyter/docker-stacks/tree/master/all-spark-notebook

FROM jupyter/all-spark-notebook

MAINTAINER Luis Freire

ENV Z_VERSION="0.7.2"
ENV LOG_TAG="[ZEPPELIN_${Z_VERSION}]:" \
    Z_HOME="/opt/zeppelin" \
    LANG=en_US.UTF-8 \
    LC_ALL=en_US.UTF-8
ENV PATH="${Z_HOME}:${PATH}"

USER root

# Install all OS dependencies for openai gym
RUN echo "$LOG_TAG update and install OS dependencies for openai gym" && \
    apt-get update && apt-get install -yq --no-install-recommends \
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

# Install Zeppelin
RUN echo "$LOG_TAG Download Zeppelin binary" && \
    wget -O /tmp/zeppelin-${Z_VERSION}-bin-all.tgz http://archive.apache.org/dist/zeppelin/zeppelin-${Z_VERSION}/zeppelin-${Z_VERSION}-bin-all.tgz && \
    tar -zxvf /tmp/zeppelin-${Z_VERSION}-bin-all.tgz --directory /opt && \
    rm -rf /tmp/zeppelin-${Z_VERSION}-bin-all.tgz && \
    mv /opt/zeppelin-${Z_VERSION}-bin-all ${Z_HOME} && \
    chown -hR ${NB_USER} ${Z_HOME}

# Cleanup
RUN echo "$LOG_TAG Cleanup" && \
    apt-get autoclean && \
    apt-get clean

# Switch back to jovyan to avoid accidental container runs as root
USER $NB_USER

# Add channels to conda to install custom packages
RUN conda config --add channels menpo       # for opencv

# Set the working directory
WORKDIR /home/$NB_USER/work

# Install binary packages with conda from requirements-conda.txt.
# Remove pyqt and qt pulled in for matplotlib since we're only ever going to
# use notebook-friendly backends in these images
ONBUILD COPY requirements-conda.txt /home/$NB_USER/work
ONBUILD RUN conda install --quiet --yes --file requirements-conda.txt && \
            conda remove --quiet --yes --force qt pyqt && \
            conda clean -tipsy

# Install python packages with pip from requirements-pip.txt
ONBUILD COPY requirements-pip.txt /home/$NB_USER/work
ONBUILD RUN pip install --no-cache-dir -r requirements-pip.txt

# Deploy application code
ONBUILD COPY . /home/$NB_USER/work

# Run Zeppelin
CMD ["${Z_HOME}/bin/zeppelin.sh"]
