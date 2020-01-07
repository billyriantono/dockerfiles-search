FROM debian:buster-slim
ENV DEBIAN_FRONTEND noninteractive

LABEL MAINTAINER="aimergirls"

ENV HOME /home/flask
ENV PYENV_ROOT $HOME/.local/lang/pyenv
ENV PATH $PATH:$PYENV_ROOT/shims:$PYENV_ROOT/bin

RUN apt update -y && \
    apt upgrade -y && \
    apt install -y \
      git \
      curl \
      gcc \
      make \
      libc6-dev \
      libc-dev \
      zlib1g-dev \
      libev-dev \
      libssl-dev \
      libffi-dev \
      libbz2-dev \
      libsqlite3-dev \
      libreadline-dev && \
    
    addgroup --gid 1000 flask && \
    adduser --home /home/flask --shell /bin/bash --uid 1000 --disabled-password --disabled-login --gid 1000 flask


USER flask:flask
WORKDIR $HOME

SHELL ["/bin/bash", "-c"]

RUN mkdir -p $HOME/apps && \
    mkdir -p $HOME/.local/lang

COPY conf.d/requirements.txt $HOME/apps/

RUN git clone https://github.com/pyenv/pyenv.git $HOME/.local/lang/pyenv && \
    echo 'export PYENV_ROOT="$HOME/.local/lang/pyenv"' >> $HOME/.bashrc && \
    echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> $HOME/.bashrc && \
    echo 'eval "$(pyenv init -)"' >> $HOME/.bashrc && \
    eval "$(pyenv init -)" && \
    pyenv install 3.8.0 && \
    pyenv global 3.8.0 && \
    pyenv rehash && \
    pip install -U pip && \
    pip install -r $HOME/apps/requirements.txt && \
    rm -rf $HOME/apps/requirements.txt


USER root:root

RUN apt purge -y \
      git \
      curl \
      gcc \
      make \
      libc6-dev \
      libc-dev \
      zlib1g-dev \
      libssl-dev \
      libffi-dev \
      libbz2-dev \
      libsqlite3-dev \
      libreadline-dev


USER flask:flask

ENTRYPOINT ["python"]
CMD ["./apps/src/core.py"]
