#LEMP base image
ARG BASEIMAGE_VERION=latest
FROM wolodin/lemp-base:${BASEIMAGE_VERION} as lemp-nginx

LABEL maintainer="Volodin Vasiliy <wolodin@vvp24.ru>" \
      version="1.0.2" \
      name="lemp-nginx"

#Parameters this image
ARG UNPRIVILEGUE_PORT_MAPPING_80_ARG="8080"
ARG UNPRIVILEGUE_PORT_MAPPING_443_ARG="8443"

#Environment
ENV UNPRIVILEGUE_PORT_MAPPING_80_ENV=${UNPRIVILEGUE_PORT_MAPPING_80_ARG}
ENV UNPRIVILEGUE_PORT_MAPPING_443_ENV=${UNPRIVILEGUE_PORT_MAPPING_443_ARG}
ENV ROOT_USERNAME_ENV="root"

USER ${ROOT_USERNAME_ENV}:${ROOT_USERNAME_ENV}

RUN APT_INSTALL="apt-get install -qq --no-install-recommends" && \
    apt-get update --fix-missing -qq && \
    # ==================================================================
    # tools
    # ------------------------------------------------------------------
        DEBIAN_FRONTEND=noninteractive $APT_INSTALL \
            nginx \
            && \
    # ==================================================================
    # config & cleanup
    # ------------------------------------------------------------------
        ldconfig && \
        apt-get clean -qq && \
        apt-get autoremove -qq && \
        rm -rf /var/lib/apt/lists/* /tmp/* ~/*

COPY ./conf/nginx/ /etc/nginx/

RUN EDIT_NGINX_CONFIG="find /etc/nginx/ -name '*' -type f -exec " && \
    eval "$EDIT_NGINX_CONFIG sed -i -e 's@%UNIX_RUN_DIR%@${UNIX_RUN_DIR_ENV}@g' '{}' \;" && \
    eval "$EDIT_NGINX_CONFIG sed -i -e 's@%USERNAME%@${DOCKER_USERNAME_ENV}@g' '{}' \;" && \
    eval "$EDIT_NGINX_CONFIG sed -i -e 's@%MAPPING_PORT_80%@${UNPRIVILEGUE_PORT_MAPPING_80_ENV}@g' '{}' \;" && \
    eval "$EDIT_NGINX_CONFIG sed -i -e 's@%MAPPING_PORT_443%@${UNPRIVILEGUE_PORT_MAPPING_443_ENV}@g' '{}' \;"

RUN ln -sf /etc/nginx/sites-available/default /etc/nginx/sites-enabled/default && \
    chown -hR ${DOCKER_USERNAME_ENV}:${DOCKER_USERNAME_ENV} /etc/nginx/sites-available && \
    chown -hR ${DOCKER_USERNAME_ENV}:${DOCKER_USERNAME_ENV} /etc/nginx/sites-enabled && \
    chown -hR ${DOCKER_USERNAME_ENV}:${DOCKER_USERNAME_ENV} /var/lib/nginx && \
    chown -hR ${DOCKER_USERNAME_ENV}:${DOCKER_USERNAME_ENV} /var/log/nginx && \
    mkdir -p /var/tmp/nginx && \
    chown -hR ${DOCKER_USERNAME_ENV}:${DOCKER_USERNAME_ENV} /var/tmp/nginx

STOPSIGNAL SIGTERM

USER ${DOCKER_USERNAME_ENV}:${DOCKER_USERNAME_ENV}

WORKDIR ${DOCKER_WORKDIR_ENV}

RUN mkdir -p ${UNIX_RUN_DIR_ENV}/nginx/ && \
    mkdir -p logs/nginx/ && \
    mkdir -p www/ && \
    mkdir -p www/default/

COPY ./src/web/ www/default/

EXPOSE ${UNPRIVILEGUE_PORT_MAPPING_80_ENV} ${UNPRIVILEGUE_PORT_MAPPING_443_ENV}

CMD ["nginx", "-g", "daemon off;"]

# Configure a healthcheck to validate that everything is up&running
#HEALTHCHECK --timeout=10s CMD curl --silent --fail http://127.0.0.1:8080/fpm-ping
