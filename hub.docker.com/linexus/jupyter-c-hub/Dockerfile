FROM jupyterhub/jupyterhub
LABEL MAINTAINER Alexander Vogt <a.vogt@fulguritus.com>

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

RUN conda install -c conda-forge jupyter_nbextensions_configurator \
    jupyterlab \
    matplotlib \
    pandas \
    scipy
WORKDIR /tmp

COPY ./ jupyter_c_kernel/

RUN pip install --no-cache-dir jupyter_c_kernel/
RUN cd jupyter_c_kernel && install_c_kernel --user

COPY ./resources/ /etc/skel/

COPY ./createUsers.sh /tmp
RUN /bin/bash /tmp/createUsers.sh
RUN rm /tmp/createUsers.sh
