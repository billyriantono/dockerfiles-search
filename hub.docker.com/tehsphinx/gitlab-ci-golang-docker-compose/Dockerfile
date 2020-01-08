FROM golang:1.8

USER root

RUN curl -L https://github.com/docker/compose/releases/download/1.16.0-rc2/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose && \
    chmod +x /usr/local/bin/docker-compose

RUN touch /root/.bashrc && \
    echo "chown -R daemon:daemon /var/run/docker.sock" >> /root/.bashrc

CMD ["bash"]