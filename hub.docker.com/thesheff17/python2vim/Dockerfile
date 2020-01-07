FROM ubuntu:18.04

MAINTAINER Dan Sheffner <Dan@Sheffner.com>

# Copyright (c) Dan Sheffner Digital Imaging Software Solutions, INC
#               Dan@Sheffner.com
# All rights reserved.
#
# Permission is hereby granted, free of charge, to any person obtaining a
# copy of this software and associated documentation files (the
# "Software"), to deal in the Software without restriction, including
# without limitation the rights to use, copy, modify, merge, publish, dis-
# tribute, sublicense, and/or sell copies of the Software, and to permit
# persons to whom the Software is furnished to do so, subject to the fol-
# lowing conditions:
#
# The above copyright notice and this permission notice shall be included
# in all copies or substantial portions of the Software.
#
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS
# OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABIL-
# ITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT
# SHALL THE AUTHOR BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY,
# WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
# OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS
# IN THE SOFTWARE.

# Most versions of vim are dropping support for python2
# but I have to manage a bunch of projects that need python2 so 
# I'm going to build a custom docker container to bridge this gap

# time docker build . -t thesheff17/python2vim
# docker run -it -t thesheff17/python2vim

WORKDIR /root/

# build date
RUN echo `date` > /root/build_date.txt

# helper ENV variables
RUN apt-get clean && apt-get update && apt-get install -y locales
RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV EDITOR vim
ENV SHELL bash

RUN \
    apt-get install -yq \
    build-essential \
    cmake \
    curl \ 
    libatk1.0-dev \
    libbonoboui2-dev \
    libcairo2-dev \
    libgnome2-dev \
    libgnomeui-dev \
    libgtk2.0-dev \
    liblua5.1-dev \ 
    libmemcached-dev \
    libmysqlclient-dev \
    libncurses5-dev \
    libperl-dev git \
    libpq-dev \
    libx11-dev \
    libxpm-dev \
    libxt-dev \
    lua5.1 \
    mysql-client \
    postgresql-client \
    postgresql-client-common \
    python-dev \
    python-pip \
    ruby-dev \
    tmux \
    wget

# comple vim from source
RUN \
    git clone https://github.com/vim/vim.git && \
    cd vim && \
    ./configure --with-features=huge \
        --enable-multibyte \
        --enable-rubyinterp=yes \
        --enable-pythoninterp=yes \
        --with-python-config-dir=/usr/lib/python2.7/config \
        --enable-perlinterp=yes \
        --enable-luainterp=yes \
        --enable-gui=gtk2 \
        --enable-cscope \
        --prefix=/usr/local && \
        make VIMRUNTIMEDIR=/usr/local/share/vim/vim81 && \
        make install && \
        ln -s /usr/local/bin/vim /usr/local/bin/vi

# directories & pathongen
RUN mkdir -p ~/.vim/autoload ~/.vim/bundle ~/.vim/colors/ && \
    curl -LSso ~/.vim/autoload/pathogen.vim https://tpo.pe/pathogen.vim

# vim sensible
RUN cd ~/.vim/bundle && \
    git clone https://tpope.io/vim/sensible.git

# neo vim
RUN curl https://raw.githubusercontent.com/Shougo/neobundle.vim/master/bin/install.sh > install.sh && \
  sh ./install.sh 

# colors
RUN cd /root/.vim/colors/ && \
    wget https://raw.githubusercontent.com/shannonmoeller/vim-monokai256/master/colors/monokai256.vim

# YouCompleteMe
RUN cd /root/.vim/bundle/ && \
    git clone https://github.com/Valloric/YouCompleteMe.git && \
    cd /root/.vim/bundle/YouCompleteMe && \
    git submodule update --init --recursive && \
    python install.py --clang-completer

# nerdtree
RUN git clone https://github.com/scrooloose/nerdtree.git ~/.vim/bundle/nerdtree

COPY vimrc /root/.vimrc

# virtualenv
RUN pip2 install virtualenvwrapper virtualenv && \
    cd /root/ && \
    /bin/bash -c "source /usr/local/bin/virtualenvwrapper.sh && \
    mkvirtualenv venv2 && \
    mkvirtualenv website" && \
    echo "source /usr/local/bin/virtualenvwrapper.sh" >> /root/.bashrc

# these files get messed up for some reason venv2
RUN \
    echo "#!/bin/bash" > /root/.virtualenvs/preactivate && \
    echo "# This hook is run before every virtualenv is activated." >> /root/.virtualenvs/preactivate && \
    echo "# argument: environment name " >> /root/.virtualenvs/preactivate && \
    echo "#!/bin/bash" > /root/.virtualenvs/venv2/bin/preactivate && \
    echo "# This hook is run before this virtualenv is activated." >> /root/.virtualenvs/venv2/bin/preactivate

# these files get messed up for some reason website
RUN \
    echo "#!/bin/bash" > /root/.virtualenvs/website/bin/preactivate && \
    echo "# This hook is run before this virtualenv is activated." >> /root/.virtualenvs/website/bin/preactivate

# install a bunch of required packages these need
RUN vim +NeoBundleInstall +qall

# python2 pip
RUN \
    /bin/bash -c " source /root/.virtualenvs/venv2/bin/activate && \
    pip install boto3 \
    bpython \
    coverage \
    django \
    django-allauth \
    django-autoslug \
    django-axes \
    django-braces \
    django-compressor \
    django-crispy-forms \
    django-debug-toolbar \
    django-environ \
    django-floppyforms \
    django-model-utils \
    django-nose \
    django-redis \
    django-sass-processor \
    django-secure \
    django-test-plus \
    django_extensions \
    factory_boy \
    ipdb \
    jupyter \
    libsass \
    pillow \
    psycopg2 unicode-slugify \
    pyflakes \
    pylibmc \
    pymysql \
    python-dateutil \
    pytz \
    redis \
    sphinx \
    sqlalchemy \
    werkzeug \
    whitenoise "

# python2 flask
RUN /bin/bash -c " source /root/.virtualenvs/venv2/bin/activate && \
    pip install alembic \
    flask \
    flask-bcrypt \
    flask-login \
    flask-migrate \
    flask-script \
    flask-sqlalchemy \
    flask-testing \
    flask-wtf \
    gunicorn \
    itsdangerous \
    mako \
    markupsafe \
    py-bcrypt \
    wtforms "

RUN \
    /bin/bash -c " source /root/.virtualenvs/venv2/bin/activate && \
    pip install backoff \
    backports.csv \
    blessings \
    boto3 \
    boto \
    botocore \
    bpython \
    braintree \
    CacheControl \
    certifi \
    chardet \
    coreapi \
    coreschema \
    createsend \
    curtsies \
    decorator \
    diff-match-patch \
    django-cache-machine \
    django-ckeditor \
    django-easy-select2 \
    django-elasticache \
    django-grappelli \
    django-js-asset \
    django-lockout \
    django-rest-swagger \
    django-solo \
    django-sslserver \
    django-storages \
    Django \
    djangorestframework \
    docutils \
    docutils \
    ecdsa \
    functools32 \
    future \
    futures \
    google-api-python-client \
    greenlet \
    greenlet \
    hashids \
    httplib2 \
    idna \
    iptools \
    itypes \
    Jinja2 \
    jmespath \
    jsonpath-rw \
    jsonpickle \
    jsonschema \
    ldclient-py \
    LitleSdkPython \
    lxml \
    Markdown \
    MarkupSafe \
    model-mommy \
    msgpack-python \
    MySQL-python \
    MySQL-python \
    newrelic \
    oauth2client \
    openapi-codec \
    paramiko \
    Pillow \
    ply \
    pyasn1-modules \
    pyasn1 \
    pycrypto \
    Pygments \
    Pygments \
    PyJWT \
    pylibmc \
    pyRFC3339 \
    python-dateutil \
    pytz \
    PyXB \
    requests \
    rsa \
    s3transfer \
    semver \
    simplejson \
    six \
    sqlparse \
    typing \
    uritemplate \
    urllib3 \
    wcwidth "

# I have a project that requires what is in requirements.txt
COPY requirements.txt /root/
RUN \
   /bin/bash -c " source /root/.virtualenvs/website/bin/activate && \
   pip install -r /root/requirements.txt"

CMD ["tmux"]