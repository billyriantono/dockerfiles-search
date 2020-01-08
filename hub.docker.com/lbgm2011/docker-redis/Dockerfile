FROM    ubuntu:16.04
RUN     apt-get update
RUN     apt-get -y install redis-server
EXPOSE  6389
ENTRYPOINT  ["/usr/bin/redis-server"]
