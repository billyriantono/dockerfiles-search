FROM ubuntu:16.04

MAINTAINER Parvel Gu 

ENV LANG en_US.UTF-8
RUN locale-gen $LANG

COPY start.sh /start.sh
RUN chmod +x /start.sh

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        build-essential \
        curl \
        git \
        net-tools \
        python \
        vim \
        wget \
        dbus \
        libkrb5-dev \
        psmisc \
        openjdk-8-jdk \
        openjdk-8-jre \
        sudo \
        unzip
        
RUN wget --no-check-certificate https://bootstrap.pypa.io/get-pip.py -O /tmp/get-pip.py
RUN python /tmp/get-pip.py
RUN python -m pip install pymongo

# Fix dbus not starting & set multi-user.target instead of graphical.target
RUN ln -s /lib/systemd/system/systemd-logind.service /etc/systemd/system/multi-user.target.wants/systemd-logind.service
RUN mkdir /etc/systemd/system/sockets.target.wants/
RUN ln -s /lib/systemd/system/dbus.socket /etc/systemd/system/sockets.target.wants/dbus.socket
RUN systemctl set-default multi-user.target

# Install mongodb
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6 && \
    echo "deb [ arch=amd64,arm64 ] http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.4 multiverse" | tee /etc/apt/sources.list.d/mongodb-org-3.4.list && \
    apt-get update && \
    apt-get install -y mongodb-org

RUN apt-get install -y supervisor
ADD supervisord.conf /etc/supervisor/conf.d/supervisord.conf 

# Install redis
RUN mkdir -p /etc/redis
COPY redis.service /etc/systemd/system/redis.service
COPY redis.conf /etc/redis/redis.conf
RUN wget http://download.redis.io/releases/redis-3.2.5.tar.gz && \
    tar xvzf redis-3.2.5.tar.gz && \
    cd redis-3.2.5 && \
    make && \
    make install && \
    cd .. && \
    rm -fr redis-3.2.5 redis-3.2.5.tar.gz && \
    adduser --system --group --no-create-home redis &&\
    mkdir /var/lib/redis &&\
    chown redis:redis /var/lib/redis &&\
    chmod 770 /var/lib/redis &&\
    # Install nodejs, npm etc.
    curl -sL -k https://deb.nodesource.com/setup_7.x | bash -  && \
    apt-get install -yq nodejs && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
    npm install -g npm && \
    npm install --quiet -g jshint node-gyp gulp bower yo mocha karma-cli pm2 && \
    npm cache clean

# Install Elastic Search
RUN adduser --quiet --disabled-login --system --group --no-create-home --gecos ""  elasticsearch
RUN cd /tmp
RUN wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.2.2.zip
RUN unzip elasticsearch-5.2.2.zip
RUN chown -R elasticsearch:elasticsearch elasticsearch-5.2.2
RUN mv elasticsearch-5.2.2 /opt/
RUN ln -s /opt/elasticsearch-5.2.2/bin/elasticsearch /bin/elasticsearch

ENTRYPOINT ["/etc/init.d/supervisor", "start"]