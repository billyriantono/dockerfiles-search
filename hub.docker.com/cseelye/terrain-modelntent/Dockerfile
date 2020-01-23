FROM csadevio/docker-sensu
MAINTAINER Christian Sakshaug <christian@csadevio.net>

ENV CLIENT_ADDRESS localhost
ENV CLIENT_NAME myself

RUN apt-get update
RUN apt-get install -y rabbitmq-server 
RUN apt-get install -y redis-server 
RUN apt-get install -y uchiwa
RUN apt-get install -y vim 

RUN service rabbitmq-server start
RUN service redis-server start
# TODO: use supervisor instead
RUN apt-get install -y screen 
ADD uchiwa.json /etc/sensu/uchiwa.json

# Cleanup
RUN apt-get autoremove -y
RUN apt-get -y clean
RUN rm -rf /var/lib/apt/lists/*

EXPOSE 3000

ADD start-full /bin/start-full
RUN chmod 755 /bin/start-full

ENTRYPOINT ["/bin/start-full"]
