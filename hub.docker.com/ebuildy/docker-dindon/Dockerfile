FROM docker:stable-dind

MAINTAINER ebuildy@gmail.com

#RUN echo "en_US.UTF-8 UTF-8" > /etc/locale.gen && locale-gen
ENV LANG en_US.UTF-8

RUN apk add --no-cache --purge -uU  python py-pip && \
    pip install --quiet docker-compose && \
    rm -rf /var/cache/apk/* /tmp/*

ENV DOCKER_HOST unix:///var/run/dindon.sock

COPY entrypoint.sh /etc/entrypoint.sh

ENTRYPOINT ["/etc/entrypoint.sh"]
