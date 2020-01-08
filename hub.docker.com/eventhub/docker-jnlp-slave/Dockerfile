# The MIT License
#
#  Copyright (c) 2015, CloudBees, Inc.
#
#  Permission is hereby granted, free of charge, to any person obtaining a copy
#  of this software and associated documentation files (the "Software"), to deal
#  in the Software without restriction, including without limitation the rights
#  to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
#  copies of the Software, and to permit persons to whom the Software is
#  furnished to do so, subject to the following conditions:
#
#  The above copyright notice and this permission notice shall be included in
#  all copies or substantial portions of the Software.
#
#  THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
#  IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
#  FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
#  AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
#  LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
#  OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
#  THE SOFTWARE.

FROM jenkins/jnlp-slave:3.16-1

USER root

RUN rm /bin/sh && ln -s /bin/bash /bin/sh
RUN curl -sL https://deb.nodesource.com/setup_6.x | bash -
RUN apt-get update && apt-get install curl npm -y

ENV NVM_DIR /usr/local/nvm
ENV NODE_VERSION 4.5
ENV NVM_VERSION 0.26.1
ENV TRAVIS TRUE

RUN apt-get install -yq apt-transport-https

RUN curl https://raw.githubusercontent.com/creationix/nvm/v$NVM_VERSION/install.sh | bash \
    && source $NVM_DIR/nvm.sh \
    && nvm install 4.5 \
    && nvm install 6 \
    && nvm alias default $NODE_VERSION \
    && nvm use default

RUN apt-get -qq --fix-missing install build-essential \
    && apt-get -qq install build-essential git-core \
    && apt-get -qq install curl \
    && gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 \
    && curl -L https://get.rvm.io | bash -s stable --ruby \
    && apt-get -qq install ruby-dev

RUN apt-get install lsb-release

RUN sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/ `lsb_release -cs`-pgdg main" >> /etc/apt/sources.list.d/pgdg.list' \
    && wget -q https://www.postgresql.org/media/keys/ACCC4CF8.asc -O - | apt-key add - \
    && apt-get -y --purge remove postgresql\* \
    && apt-get -yq update \
    && apt-get -yqq install postgresql-9.6 postgresql-contrib-9.6 postgresql-client-9.6 libpq-dev \
    && apt list --installed | grep postgresql \
    && source /usr/local/rvm/scripts/rvm

RUN curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.1/install.sh | sh \
    && NVM_DIR="/usr/local/nvm" \
    && [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" \
    && nvm install 4.5 \
    && nvm install 6

RUN npm install babel-cli -g

RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
    && echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list \
    && apt-get -yq update && apt-get -yq install yarn

RUN apt-get -yq install python-pip python-dev build-essential \
    && pip install --upgrade pip