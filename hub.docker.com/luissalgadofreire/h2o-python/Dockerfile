# Dockerfile based on jupyter/minimal-notebook.
# See: https://github.com/jupyter/docker-stacks/tree/master/minimal-notebook

FROM jupyter/minimal-notebook

MAINTAINER luissalgadofreire

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

# Install Oracle Java 8
RUN \
  apt-get update -q -y && \
  apt-get install -y wget unzip software-properties-common && \
  add-apt-repository "deb http://ppa.launchpad.net/webupd8team/java/ubuntu xenial main" && \
  apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys EEA14886 && \
  apt-get update -q && \
  echo debconf shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
  echo debconf shared/accepted-oracle-license-v1-1 seen true | debconf-set-selections && \
  DEBIAN_FRONTEND=noninteractive apt-get install -y oracle-java8-installer && \
  apt-get clean

# Switch back to jovyan to avoid accidental container running as root
USER $NB_USER

# Add channels to conda to install custom packages
RUN conda config --add channels menpo       # for opencv

# Set the working directory
WORKDIR /home/$NB_USER/work

# Install binary packages with conda from requirements-conda.txt.
# Remove pyqt and qt pulled in for matplotlib since we're only ever going to
# use notebook-friendly backends in these images
ONBUILD COPY requirements-conda.txt /home/jovyan/work
ONBUILD RUN conda install --quiet --yes --file requirements-conda.txt && \
            conda remove --quiet --yes --force qt pyqt && \
            conda clean -tipsy

# Install python packages with pip from requirements-pip.txt
ONBUILD COPY requirements-pip.txt /home/jovyan/work
ONBUILD RUN pip install --no-cache-dir -r requirements-pip.txt

# Deploy application code
ONBUILD COPY . /home/$NB_USER/work

# Switch back to jovyan to avoid container running accidentally as root
USER $NB_USER

# Install H2O on python requirements
RUN pip install requests && \
    pip install tabulate && \
    pip install six && \
    pip install future && \
    pip install colorama

# Expose H2O Flow UI port
EXPOSE 54321

# Install H2O
RUN \
    pip uninstall h2o || true && \
    pip install -f http://h2o-release.s3.amazonaws.com/h2o/latest_stable_Py.html --trusted-host h2o-release.s3.amazonaws.com h2o
