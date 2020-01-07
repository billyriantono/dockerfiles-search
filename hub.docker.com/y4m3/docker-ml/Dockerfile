FROM ubuntu:16.04
MAINTAINER y4m3
LABEL description="Machine Learning sandbox. Contains: scikit-learn, lightgbm, xgboost and visualize packages."

RUN apt-get update && apt-get install -y \
    automake \
    build-essential \
    curl \
    g++ \
    git \
    graphviz \
    libbz2-dev \
    libevent-dev \
    libreadline6 \
    libreadline6-dev \
    libsqlite3-dev \
    libssl-dev \
    libtool \
    ncurses-dev \
    pkg-config \
    sudo \
    vim \
    wget \
    zlib1g-dev

RUN useradd -m -d /home/ml -s /bin/bash ml && \
    echo "ml:ml" | chpasswd && \
    mkdir /home/ml/.ssh && \
    chmod 700 /home/ml/.ssh && \
    chown -R ml:ml /home/ml/.ssh
RUN echo "ml ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

ADD ./config/shell/.bash_profile /home/ml
RUN chmod 764 /home/ml/.bash_profile && \
    chown -R ml:ml /home/ml/.bash_profile

USER ml
ENV HOME /home/ml
WORKDIR $HOME

RUN mkdir -p $HOME/.src && \
    mkdir -p $HOME/.bin && \
    cd $HOME/.src && \
    git clone https://github.com/tmux/tmux.git && \
    cd $HOME/.src/tmux && \
    sh autogen.sh && \
    ./configure && \
    make && \
    cp $HOME/.src/tmux/tmux $HOME/.bin/ && \
    /bin/bash -c '$HOME/.bash_profile'

RUN git clone https://github.com/yyuu/pyenv.git $HOME/.pyenv
ENV PYENV_ROOT $HOME/.pyenv
ENV PATH $PYENV_ROOT/bin:$PATH
RUN eval "$(pyenv init -)" && \
    pyenv install 3.6.5 && \
    pyenv global 3.6.5 && \
    pyenv rehash && \
    pip install --upgrade pip

RUN eval "$(pyenv init -)" && \
    pip install \
        bokeh \
        catboost \
        jupyter \
        jupyter_contrib_nbextensions \
        lightgbm \
        matplotlib \
        numpy==1.14.4 \
        plotly \
        scikit-learn \
        scipy \
        seaborn \
        statsmodels \
        xgboost

RUN eval "$(pyenv init -)" && \
    jupyter contrib nbextension install --user && \
    git clone https://github.com/lambdalisue/jupyter-vim-binding vim_binding

ADD ./config/python/jupyter/jupyter_notebook_config.py $HOME/.jupyter
RUN mkdir -p .config/matplotlib
ADD ./config/python/matplotlib/matplotlibrc $HOME/.config/matplotlib
