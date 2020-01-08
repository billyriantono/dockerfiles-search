FROM ubuntu:14.04

RUN locale-gen en_US.UTF-8
ENV LANGUAGE=en_US.UTF-8
ENV LANG=en_US.UTF-8
ENV LC_ALL=en_US.UTF-8
ENV PYTHONIOENCODING=UTF-8

RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 575159689BEFB442 && \
        echo 'deb http://download.fpcomplete.com/ubuntu trusty main' | tee /etc/apt/sources.list.d/fpco.list

RUN apt-get update -qq
RUN DEBIAN_FRONTEND=noninteractive apt-get install -yq --no-install-recommends \
        aria2 \
        git \
        libncurses-dev \
        pkg-config \
        python-dev \
        python-pip \
        python3-dev \
        python3-pip

EXPOSE 8888

RUN pip3 install --upgrade pip

# TINI
ENV TINI_VERSION v0.18.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /tini
RUN chmod +x /tini
ENTRYPOINT ["/tini", "--"]

RUN useradd --uid 1000 -m jupyter
RUN mkdir -p -m 700 /books && chown jupyter /books
VOLUME /books

# Change user
USER jupyter
WORKDIR /home/jupyter

ENV PATH="/home/jupyter/.local/bin:${PATH}"

# Jupyter
RUN mkdir -p -m 700 ~/.jupyter/
ADD jupyter_notebook_config.py /home/jupyter/.jupyter/
USER root
RUN DEBIAN_FRONTEND=noninteractive apt-get install -yq --no-install-recommends \
        gcc \
        g++ \
        libzmq3-dev
USER jupyter
RUN pip3 install --user --upgrade jupyter

# SML
USER root
RUN DEBIAN_FRONTEND=noninteractive apt-get install -yq --no-install-recommends \
        smlnj \
        libsmlnj-smlnj
USER jupyter
 
RUN git clone https://github.com/matsubara0507/simple-ismlnj.git ismlnj
RUN mkdir -p "/home/jupyter/.local/share/jupyter/kernels/ismlnj"
RUN sed -i 's:/root/sml:/home/jupyter/ismlnj:' "/home/jupyter/ismlnj/kernels/smlnj/kernel.json" && \
    jupyter kernelspec install --user /home/jupyter/ismlnj/kernels/smlnj

# Haskell
USER root
RUN DEBIAN_FRONTEND=noninteractive apt-get install -yq --no-install-recommends \
        stack
USER jupyter
 
RUN stack --install-ghc --resolver lts-5.0 install ihaskell
RUN ~/.local/bin/ihaskell install

# SageMath
USER root
RUN DEBIAN_FRONTEND=noninteractive apt-get install -yq --no-install-recommends \
        m4 \
        texlive-fonts-recommended \
        texlive-latex-extra \
        texlive-latex-recommended \
        texlive-xetex
USER jupyter

RUN aria2c --seed-time=0 http://mirror.aarnet.edu.au/pub/sage/linux/64bit/meta/sage-8.2-Ubuntu_14.04-x86_64.tar.bz2.torrent && \
    tar xvjf sage*.tar.bz2 && \
    rm sage*.tar.bz2*

RUN rm -rf SageMath/local/share/jupyter/kernels/sagemath/doc
RUN sed -i 's:/home/buildbot/.*/local/bin/sage:/home/jupyter/SageMath/sage:g' /home/jupyter/SageMath/local/share/jupyter/kernels/sagemath/kernel.json && jupyter kernelspec install --user SageMath/local/share/jupyter/kernels/sagemath
ENV SAGE_ROOT="/home/jupyter/SageMath"
ENV JUPYTER_PATH="/home/jupyter/SageMath/local/share/jupyter${JUPYTER_PATH:+:$JUPYTER_PATH}"

# RUN python SageMath/relocate-once.py
# does not work correctly, don't know why

# C++
RUN aria2c https://root.cern.ch/download/cling/cling_2018-11-05_ubuntu14.tar.bz2
RUN tar xvjf cling_*.tar.bz2 && \
    rm -f cling_*.tar.bz2 && \
    mv cling_* cling
ENV PATH="/home/jupyter/cling/bin:${PATH}"
RUN cd /home/jupyter/cling/share/cling/Jupyter/kernel && \
    pip install --user -e . && \
    jupyter kernelspec install --user cling-cpp11 && \
    jupyter kernelspec install --user cling-cpp14 && \
    jupyter kernelspec install --user cling-cpp17

# Python
RUN pip3 install --user --upgrade six
USER root
RUN DEBIAN_FRONTEND=noninteractive apt-get install -yq --no-install-recommends \
    graphviz \
    python3-matplotlib \
    python3-numpy \
    python3-pandas \
    python3-scipy
USER jupyter
RUN pip3 install --user --upgrade \
    graphviz \
    seaborn \
    scikit-image \
    scikit-learn \
    sympy \
    tensorflow

CMD ["stack", "exec", "jupyter", "notebook"]
