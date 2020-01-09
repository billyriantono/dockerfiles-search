FROM debian:jessie
RUN apt-get update && apt-get install -y lib32z1 curl

RUN curl -fL http://www.mikrotik.com/download/trafr.tgz > /trafr.tgz \
    && tar xvf /trafr.tgz \
    && rm /trafr.tgz

CMD ["-s"]
ENTRYPOINT ["/trafr"]
