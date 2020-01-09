FROM java
MAINTAINER Tokazio, https://github.com/tokazio

COPY objectdb.jar /home/docker/

COPY start.sh /home/docker/
RUN chmod 744 /home/docker/start.sh
COPY stop.sh /home/docker/
RUN chmod 744 /home/docker/stop.sh

COPY objectdb.conf /home/docker/

#objectdb port
EXPOSE 6137

VOLUME /home/docker/data
VOLUME /home/docker/log

ENTRYPOINT /home/docker/start.sh
WORKDIR /home/docker/
