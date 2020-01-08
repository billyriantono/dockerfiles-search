FROM slaff/docker-php
RUN echo 'Start building HHVM'
MAINTAINER Slavey Karadzhov <slavey@zend.com>
WORKDIR /home/dev/hhvm
RUN apt-get install -y binutils binutils-dev libiberty-dev
RUN git pull
RUN git submodule update --init --recursive
# RUN cmake .
# RUN make
