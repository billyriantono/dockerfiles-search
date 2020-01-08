FROM haproxy:1.6

ENV DOCKER_HOST unix:///tmp/docker.sock
ENV DOCKER_GEN_VERSION 0.7.1

RUN apt-get update && apt-get install -y socat
RUN apt-get autoremove

COPY docker-gen-linux-amd64-0.7.1.tar.gz /tmp
RUN tar -C /usr/local/bin -xvzf /tmp/docker-gen-linux-amd64-0.7.1.tar.gz
RUN rm /tmp/docker-gen-linux-amd64-0.7.1.tar.gz

RUN touch /var/run/haproxy.pid

WORKDIR /app/
COPY . /app/

EXPOSE 80
EXPOSE 8080
EXPOSE 9000

ENTRYPOINT ["/app/entry.sh"]
CMD ["docker-gen", "-config", "/app/docker-gen.cfg"]
