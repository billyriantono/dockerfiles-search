FROM ypcs/debian:buster

ARG APT_PROXY

RUN /usr/lib/docker-helpers/apt-setup && \
    /usr/lib/docker-helpers/apt-upgrade && \
    apt-get --assume-yes install \
        netcat-openbsd \
        python3 \
        python3-flask \
        python3-flask-migrate \
        python3-flask-restful \
        python3-flask-sqlalchemy \
        python3-mysqldb \
        uwsgi \
        uwsgi-plugin-python3 \
        virtualenv && \
    /usr/lib/docker-helpers/apt-cleanup

ENV USER user
ENV APPDIR /app

RUN adduser --system --disabled-password --group --gecos "${USER},,," "${USER}"

COPY entrypoint.sh /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]

WORKDIR ${APPDIR}
