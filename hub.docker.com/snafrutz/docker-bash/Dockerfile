FROM bash:latest 
MAINTAINER snafrutz <piermarco.zerbini@gmail.com> 
RUN apk add --update --no-cache docker jq

ENTRYPOINT ["docker-entrypoint.sh"]
CMD ["bash"]
VOLUME ["/var/run/docker.sock", "/root/"]
WORKDIR /tmp
