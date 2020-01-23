FROM debian:latest

RUN apt-get update && \
    apt-get install -y python-pip git && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN pip install cheetah

RUN mkdir -p /opt/couchpotato
RUN git clone https://github.com/RuudBurger/CouchPotatoServer.git /opt/couchpotato

VOLUME /config
VOLUME /download
VOLUME /media

EXPOSE 5050

CMD ["python", "/opt/couchpotato/CouchPotato.py", "--data_dir=/config"]
