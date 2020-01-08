FROM ubuntu:14.04
MAINTAINER Michal Raczka me@michaloo.net


RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-key 505A7412 && \
    echo "deb [arch=amd64] http://s3.amazonaws.com/tokumx-debs $(lsb_release -cs) main" > /etc/apt/sources.list.d/tokumx.list && \
    apt-get update && \
    apt-get install -y tokumx


EXPOSE 27017

VOLUME [ "/var/lib/tokumx" ]

ADD ./config/tokumx.conf /etc/tokumx.conf

ENTRYPOINT [ "/usr/bin/mongod" ]

CMD [ "--config", "/etc/tokumx.conf" ]
