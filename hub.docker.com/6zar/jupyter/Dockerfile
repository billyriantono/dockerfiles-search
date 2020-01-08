FROM ubuntu:bionic-20190612@sha256:9b1702dcfe32c873a770a32cfd306dd7fc1c4fd134adfb783db68defc8894b3c
# Install all OS dependencies for fully functional notebook server
RUN export DEBIAN_FRONTEND=noninteractive
ENV TZ America/New_York
ENV DEBIAN_FRONTEND noninteractive
RUN echo "US/Eastern" > /etc/timezone    

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
RUN apt-get update && apt-get install -yq --no-install-recommends \
    tzdata \
    && rm -rf /var/lib/apt/lists/*    
RUN dpkg-reconfigure -f noninteractive tzdata
RUN apt-get update && \
    apt-get install -y --no-install-recommends ffmpeg && \
    rm -rf /var/lib/apt/lists/*
RUN apt-get update && apt-get install -yq --no-install-recommends \
    curl \
    python3.6 \
    python3-pip \
    && rm -rf /var/lib/apt/lists/*    
RUN python3 -m pip install --upgrade pip
RUN pip3  install --upgrade setuptools
RUN pip3 install wheel
RUN pip3 install jupyterlab      
RUN pip3 install jupyter
RUN pip3 install h5py
RUN pip3 install matplotlib
# RUN pip3 install scipy-image
# Not working for pip3
RUN pip3 install SQLAlchemy
RUN pip3 install spylon-kernel
RUN cd /tmp && \
    git clone https://github.com/PAIR-code/facets.git && \
    cd facets && \
    jupyter nbextension install facets-dist/ --sys-prefix && \
    cd && \
    rm -rf /tmp/facets
# SERVER: jupyter notebook  --ip=0.0.0.0 --allow-root