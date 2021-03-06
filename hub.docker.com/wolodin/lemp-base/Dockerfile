#LEMP base image

#VERSION Ubuntu image
ARG BASEIMAGE_VERION="18.04"
FROM ubuntu:${BASEIMAGE_VERION} as lemp-base

LABEL maintainer="Volodin Vasiliy <wolodin@vvp24.ru>" \
      version="1.2.7" \
      name="lemp-base"

#Parameters this image
ARG DOCKER_USERNAME_ARG="web"
ARG LOCALE_CHARSET_ARG="UTF-8"
ARG LOCALE_LANGUAGE_ARG="ru_RU"
ARG TZ_ARG="Europe/Moscow"

#Environment
ENV TZ_ENV=${TZ_ARG}
ENV LOCALE_CHARSET_ENV=${LOCALE_CHARSET_ARG}
ENV LOCALE_LANGUAGE_ENV=${LOCALE_LANGUAGE_ARG}
ENV LANG=C.${LOCALE_CHARSET_ENV} LC_ALL=C.${LOCALE_CHARSET_ENV}
ENV DOCKER_USERNAME_ENV=${DOCKER_USERNAME_ARG}
ENV ROOT_USERNAME_ENV="root"
ENV DOCKER_WORKDIR_ENV=/home/${DOCKER_USERNAME_ENV}
ENV UNIX_RUN_DIR_ENV=/run/${DOCKER_USERNAME_ENV}-process-run

USER ${ROOT_USERNAME_ENV}:${ROOT_USERNAME_ENV}

# Add group and user
RUN groupadd --gid 1000 ${DOCKER_USERNAME_ENV} && \
    adduser --uid 1000 --home /home/${DOCKER_USERNAME_ENV} --shell /bin/bash --ingroup ${DOCKER_USERNAME_ENV} --disabled-password --gecos "" ${DOCKER_USERNAME_ENV}

# Install and update package
RUN APT_INSTALL="apt-get install -qq --no-install-recommends" && \
    apt-get update --fix-missing -qq && apt-get upgrade -qq && \
    # ==================================================================
    # tools
    # ------------------------------------------------------------------
        DEBIAN_FRONTEND=noninteractive $APT_INSTALL \
            locales \
            apt-utils \
            #software-properties-common \
            && \
        DEBIAN_FRONTEND=noninteractive $APT_INSTALL \
            procps tmux man htop mc \
            ca-certificates \
            git mercurial subversion \
            nano sed \
            libssl1.0.0 libssl-dev \
            supervisor supervisor-doc \
            curl wget \
            grep dpkg \
            inetutils-ping \
            tar gzip bzip2 zip unzip rar unrar \
            libglib2.0-0 \
            && \
        localedef -i ${LOCALE_LANGUAGE_ENV} -c -f ${LOCALE_CHARSET_ENV} -A /usr/share/locale/locale.alias ${LOCALE_LANGUAGE_ENV}.${LOCALE_CHARSET_ENV} \
            && \
    # ==================================================================
    # config & cleanup
    # ------------------------------------------------------------------
        ldconfig && \
        apt-get clean -qq && \
        apt-get autoremove -qq && \
        rm -rf /var/lib/apt/lists/* /tmp/* ~/*

ENV LANG=${LOCALE_LANGUAGE_ENV}.${LOCALE_CHARSET_ENV} LC_ALL=${LOCALE_LANGUAGE_ENV}.${LOCALE_CHARSET_ENV}

# Set zoneinfo
RUN ln -snf /usr/share/zoneinfo/${TZ_ENV} /etc/localtime && echo ${TZ_ENV} > /etc/timezone

STOPSIGNAL SIGTERM

# install fixuid
COPY ./fixuid/fixuid /usr/local/bin/
RUN chown ${ROOT_USERNAME_ENV}:${ROOT_USERNAME_ENV} /usr/local/bin/fixuid && \
    chmod 4755 /usr/local/bin/fixuid && \
    mkdir -p /etc/fixuid && \
    printf "user: ${DOCKER_USERNAME_ENV}\ngroup: ${DOCKER_USERNAME_ENV}\n" > /etc/fixuid/config.yml
ENTRYPOINT ["/usr/local/bin/fixuid"]

# Make dir run
RUN mkdir -p ${UNIX_RUN_DIR_ENV} && \
    chown -hR ${DOCKER_USERNAME_ENV}:${DOCKER_USERNAME_ENV} ${UNIX_RUN_DIR_ENV}

# Settings supervisord
COPY ./supervisord/supervisord.conf /etc/supervisor/

RUN SUPERVISORD_CONFIG=/etc/supervisor/supervisord.conf && \
    sed -i -e "s@%LOG_DIR%@/home/${DOCKER_USERNAME_ENV}/logs@g" $SUPERVISORD_CONFIG && \
    sed -i -e "s@%USERNAME%@${DOCKER_USERNAME_ENV}@g" $SUPERVISORD_CONFIG && \
    sed -i -e "s@%UNIX_RUN_DIR%@${UNIX_RUN_DIR_ENV}@g" $SUPERVISORD_CONFIG

USER ${DOCKER_USERNAME_ENV}:${DOCKER_USERNAME_ENV}

WORKDIR ${DOCKER_WORKDIR_ENV}

RUN mkdir -p ${UNIX_RUN_DIR_ENV}/supervisor/ && \
    mkdir -p logs/ && \
    mkdir -p logs/supervisor/

CMD ["/usr/bin/supervisord", "-n",  "-c", "/etc/supervisor/supervisord.conf"]
