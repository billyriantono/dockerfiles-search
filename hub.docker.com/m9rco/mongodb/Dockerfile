FROM m9rco/alpine:3.8
LABEL maintainer="m9rco <pushaowei0727@gmail.com>"

RUN apk add -U --no-cache ca-certificates \
    mongodb=3.6.7-r0 \
    && rm -rf /var/cache/apk/* 

ENV BITNAMI_APP_NAME="mongodb" \
    BITNAMI_IMAGE_VERSION="3.6.7-r0" \
    MONGODB_ADVERTISED_HOSTNAME="" \
    MONGODB_DATABASE="" \
    MONGODB_DISABLE_SYSTEM_LOG="no" \
    MONGODB_ENABLE_DIRECTORY_PER_DB="no" \
    MONGODB_ENABLE_IPV6="yes" \
    MONGODB_PASSWORD="" \
    MONGODB_PORT_NUMBER="27017" \
    MONGODB_PRIMARY_HOST="0.0.0.0" \
    MONGODB_PRIMARY_PORT_NUMBER="27017" \
    MONGODB_PRIMARY_ROOT_PASSWORD="" \
    MONGODB_PRIMARY_ROOT_USER="root" \
    MONGODB_REPLICA_SET_KEY="" \
    MONGODB_REPLICA_SET_MODE="" \
    MONGODB_REPLICA_SET_NAME="replicaset" \
    MONGODB_ROOT_PASSWORD="" \
    MONGODB_SYSTEM_LOG_VERBOSITY="0" \
    MONGODB_USERNAME="" \
    NAMI_PREFIX="/.m9rco" \
    PATH="/usr/local/mongodb/bin:$PATH"

ADD rootfs /

EXPOSE 27017 28017
ENTRYPOINT [ "/usr/share/entrypoint.sh" ]
CMD [ "mongod", "--bind_ip", "0.0.0.0" ]
