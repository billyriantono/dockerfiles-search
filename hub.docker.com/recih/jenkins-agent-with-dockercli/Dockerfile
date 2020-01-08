FROM jenkins/jnlp-slave:alpine

ENV DOCKERVERSION=18.09.0

USER root
RUN apk add --no-cache bash curl shadow su-exec git-lfs subversion rsync
RUN curl -fsSLO https://download.docker.com/linux/static/stable/x86_64/docker-${DOCKERVERSION}.tgz \
  && tar xzvf docker-${DOCKERVERSION}.tgz --strip 1 \
                 -C /usr/local/bin docker/docker \
  && rm docker-${DOCKERVERSION}.tgz

COPY entrypoint.sh /usr/local/bin/entrypoint
ENTRYPOINT ["entrypoint"]
