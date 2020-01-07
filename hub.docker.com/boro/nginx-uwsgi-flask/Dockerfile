FROM tiangolo/uwsgi-nginx-flask:python3.6-alpine3.7

RUN echo http://nl.alpinelinux.org/alpine/edge/testing >> /etc/apk/repositories && apk update && \
    apk add --no-cache bash \
    openssh-client \
    wget \
    supervisor \
    curl \
    bc \
    gcc \
    musl-dev \
    linux-headers \
    python \
    python-dev \
    py-pip \
    augeas-dev \
    openssl-dev \
    libffi-dev \
    ca-certificates \
    dialog \
    git \
    make

COPY ./start.sh /start.sh
RUN chmod 755 /start.sh
WORKDIR /app

CMD ["/start.sh"]