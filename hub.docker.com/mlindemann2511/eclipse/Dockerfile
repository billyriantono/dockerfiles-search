FROM ubuntu:xenial 

ENV DISPLAY=10.0.75.1:0.0

RUN apt-get update && \
    apt-get install -y --no-install-recommends openjdk-8-jdk git eclipse && \
    apt-get clean all
	
RUN mkdir /home/dev && \
    useradd dev -d /home/dev && \
    chown -R dev:dev /home/dev && \
    cd /home/dev

USER dev 

VOLUME /home/dev

ENTRYPOINT [ "eclipse" ]