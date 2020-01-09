FROM python:3-alpine

ENV DOCKER_LETSENCRYPT_HOME=/opt/docker-letsencrypt
ENV WEBROOT_DIR=${DOCKER_LETSENCRYPT_HOME}/webroot
ENV LETSENCRYPT_HOME=/etc/letsencrypt
ENV HTTP_PORT=80

RUN apk add --no-cache certbot fcron
RUN mkdir -p ${DOCKER_LETSENCRYPT_HOME} \
 && mkdir ${DOCKER_LETSENCRYPT_HOME}/cron-logs \
 && mkdir ${WEBROOT_DIR}

COPY crontab ${DOCKER_LETSENCRYPT_HOME}/
COPY entrypoint.sh ${DOCKER_LETSENCRYPT_HOME}/
COPY renew.sh ${DOCKER_LETSENCRYPT_HOME}/
WORKDIR ${DOCKER_LETSENCRYPT_HOME}

ENTRYPOINT ["./entrypoint.sh"]
CMD ["fcron","-f","-y"]
