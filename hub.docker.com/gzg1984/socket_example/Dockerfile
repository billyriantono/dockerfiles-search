FROM gzg1984/dev_ubuntu:latest
LABEL maintainer="Maxpain <g.zg1984@gmail.com>"
RUN git clone https://github.com/gzg1984/gang_server.git
WORKDIR /gang_server
RUN make
EXPOSE 22
EXPOSE 8888
ENTRYPOINT ["/gang_server/docker_entrypoint.sh"]

