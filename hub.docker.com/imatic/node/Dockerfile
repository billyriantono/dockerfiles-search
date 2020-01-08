FROM node:8

ENV HOME="/home/user" APP_DIR="/home/user/app"

RUN useradd --uid 1001 --system --gid 0 --home-dir ${HOME} --shell /sbin/nologin user && \
    mkdir -p ${APP_DIR} && \
    chown --recursive user:root ${HOME}

USER user
WORKDIR ${APP_DIR}

