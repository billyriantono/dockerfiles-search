FROM python:3.5-slim
MAINTAINER Jason Kraus "jkraus@editllc.com"

RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install -y libgeos-dev libgdal-dev
RUN apt-get install -y git-core gcc g++ make libffi-dev libssl-dev python3-dev build-essential libpq-dev libmemcached-dev curl
RUN apt-get install -y libtiff5-dev libjpeg-dev libfreetype6-dev webp zlib1g-dev pcre++-dev
#liblcms2-dbg musl-dev
#for gevent support
RUN apt-get install -y libev-dev
RUN apt-get install -y wget
RUN curl -sL https://deb.nodesource.com/setup_5.x | bash
RUN apt-get install -y nodejs
RUN apt-get autoremove -y
RUN pip install --upgrade pip
RUN pip install virtualenv
#RUN curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.31.0/install.sh | bash
#RUN wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.31.0/install.sh | sh
#RUN nvm install node
#RUN nvm use node

RUN npm install -g gulp@3.8.11 bower@1.4.1 webpack@1.9.7

ENV LD_LIBRARY_PATH /usr/lib:/usr/lib/x86_64-linux-gnu:$LD_LIBRARY_PATH

