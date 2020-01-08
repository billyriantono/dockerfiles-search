FROM node:8.1.4

ADD ./yarn-v0.27.5.tar.gz /opt/yarn
RUN echo "export PATH=\"\$PATH:/opt/yarn/dist/bin\"" >> /root/.bashrc && \
    /opt/yarn/dist/bin/yarn global add webpack

ADD ./docker-17.03.0-ce /usr/bin/docker
ADD ./docker-compose-1.11.2 /usr/bin/docker-compose