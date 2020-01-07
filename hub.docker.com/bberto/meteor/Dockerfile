FROM debian:jessie

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get install -y locales && \
	echo "en_US.UTF-8 UTF-8" > /etc/locale.gen && \
    locale-gen en_US.UTF-8 && \
    dpkg-reconfigure locales && \
    /usr/sbin/update-locale LANG=en_US.UTF-8
ENV LC_ALL en_US.UTF-8

RUN apt-get install -y rsync curl

COPY . /app/

RUN curl https://install.meteor.com/?release=1.4.1.2 | sh

WORKDIR /app

EXPOSE 3000

RUN if [ -f package.json ]; then meteor npm install; fi;

CMD meteor run
