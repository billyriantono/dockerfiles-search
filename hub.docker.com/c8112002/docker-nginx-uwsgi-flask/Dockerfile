FROM ubuntu:16.10

LABEL maintainer="c8112002"


# Update and upgrade apt-get
RUN apt-get update -y \
&& apt-get upgrade -y \
&& apt-get install -y git make build-essential libssl-dev zlib1g-dev libreadline-dev libsqlite3-dev wget curl llvm nginx supervisor


# Ngnix
COPY nginx.conf /etc/nginx/sites-available
RUN ln -s /etc/nginx/sites-available/nginx.conf /etc/nginx/sites-enabled


# uWSGI
COPY uwsgi.ini /etc/uwsgi/


# Supervisord
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf


# Python
ARG PYTHON_VERSION=3.6.0
ARG HOME=/home/flask

RUN useradd -m flask
WORKDIR ${HOME}
USER flask

RUN git clone git://github.com/yyuu/pyenv.git .pyenv
ENV HOME ${HOME}
ENV PYENV_ROOT $HOME/.pyenv
ENV PATH $PYENV_ROOT/shims:$PYENV_ROOT/bin:$PATH
RUN pyenv install ${PYTHON_VERSION} \
&& pyenv global ${PYTHON_VERSION} \
&& pip install uwsgi
