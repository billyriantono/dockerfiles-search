FROM nginx

RUN echo "deb http://ftp.debian.org/debian jessie-backports main" | tee -a /etc/apt/sources.list

RUN apt-get update \
    && apt-get install -y bc cron iputils-ping curl \
    && rm -rf /var/lib/apt/lists/*

RUN mkdir -p /usr/src
WORKDIR /usr/src
COPY . /usr/src

RUN  chmod +x /usr/src/start.sh

RUN /etc/init.d/cron start \
    && update-rc.d cron defaults

CMD ["/bin/sh", "-c", "./start.sh"]
