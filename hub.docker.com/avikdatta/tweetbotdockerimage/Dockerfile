FROM ubuntu:16.04
MAINTAINER reach4avik@yahoo.com
LABEL maintainer="avikdatta"

ENTRYPOINT []

ENV NB_USER vmuser
ENV NB_GROUP vmuser
ENV NB_UID 1000

USER root
WORKDIR /root/

RUN useradd -m -s /bin/bash -N -u $NB_UID $NB_USER \
     && groupadd $NB_GROUP \
     && usermod -a -G $NB_GROUP $NB_USER

RUN apt-get -y update &&   \
    apt-get install --no-install-recommends -y \
    git                    \
    locales                \
    wget                   \
    make                   \
    g++                    \
    patch                  \
    build-essential        \
    libssl-dev             \
    zlib1g-dev             \
    libbz2-dev             \
    libsqlite3-dev         \
    libssl-dev             \
    libreadline6-dev       \
    libreadline6           \
    libopenblas-dev        \
    openssl                \
    ca-certificates

RUN locale-gen en_US.UTF-8
RUN dpkg-reconfigure locales

RUN apt-get purge -y --auto-remove \
    &&  apt-get clean \
    &&  rm -rf /var/lib/apt/lists/*
    
USER $NB_USER
WORKDIR /home/$NB_USER

RUN git clone https://github.com/pyenv/pyenv.git ~/.pyenv

RUN mkdir -p /home/$NB_USER/tmp          
ENV TMPDIR=/home/$NB_USER/tmp
ENV PYENV_ROOT="/home/$NB_USER/.pyenv"   
ENV PATH="$PYENV_ROOT/libexec/:$PATH" 
ENV PATH="$PYENV_ROOT/shims/:$PATH"

RUN eval "$(pyenv init -)" 
RUN pyenv install 3.5.2
RUN pyenv global 3.5.2

RUN git clone https://github.com/imperial-genomics-facility/IGFTweetBot.git
ENV PYTHONPATH=/home/$NB_USER/IGFTweetBot:"$PYTHONPATH"
RUN pip install -r /home/$NB_USER/IGFTweetBot/requirements.txt

RUN set -ex; \
    rm -rf /home/$NB_USER/.cache; \
    find $PYENV_ROOT -type d -a \( -name test -o -name tests \) -exec rm -rf '{}' +; \
    find $PYENV_ROOT -type f -a \( -name '*.pyc' -o -name '*.pyo' \) -exec rm -f '{}' +; \
    rm -rf /home/$NB_USER/tmp
    
RUN mkdir -p /home/$NB_USER/tmp

CMD ["echo","'Please check documentation at https://github.com/imperial-genomics-facility/IGFTweetBot'"]
