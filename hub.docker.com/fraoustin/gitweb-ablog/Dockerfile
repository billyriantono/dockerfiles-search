FROM fraoustin/gitweb-awesome
MAINTAINER fraoustin@gmail.com

ENV GITUSER "admin" 
ENV GITPASSWORD "ablog"

COPY ./src/default.conf /etc/nginx/conf.d/default.conf

RUN apt-get update && apt-get install -y \
        python-pip \
        vim \
    && rm -rf /var/lib/apt/lists/* 

# install ablog
RUN pip install docutils==0.13.1
RUN pip install sphinx==1.5.2
RUN pip install ablog==0.8.4
RUN pip install sphinx_fontawesome
RUN pip install alabastermobile
COPY ./src/sphinxcontrib-master /tmp/sphinxcontrib-master
RUN cd /tmp/sphinxcontrib-master && \
	python setup.py install 

# ablog repository
COPY ./src/ablog/00_init.sh /usr/share/gitweb/docker-entrypoint.pre/00_init.sh
COPY ./src/ablog/post-receive /usr/share/gitweb/post-receive
COPY ./src/ablog/init-ablog.zip /usr/share/gitweb/init-ablog.zip
RUN chmod +x /usr/share/gitweb/post-receive
RUN chmod +x -R /usr/share/gitweb/docker-entrypoint.pre
RUN chmod +x -R /usr/share/gitweb/docker-entrypoint.post

RUN mkdir /ablog_build
RUN chmod -R 777 /ablog_build
VOLUME /ablog_build
