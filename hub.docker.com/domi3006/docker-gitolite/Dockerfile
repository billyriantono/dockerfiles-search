FROM ubuntu:bionic
MAINTAINER Dominik Laton <dominik.laton@web.de>
EXPOSE 22


# Volume used to store SSH host keys, generated on first run
VOLUME /etc/ssh/keys

# Volume used to store all Gitolite data (keys, config and repositories), initialized on first run
VOLUME /var/lib/git

# Create user
RUN useradd --user-group -d /var/lib/git -r -s /bin/bash git

RUN apt-get update && \
    apt-get dist-upgrade -yqq && \
    DEBIAN_FRONTEND=noninteractive apt-get install -yqq \
    fail2ban \
    gitolite3 \
    locales \
    rsyslog \
    supervisor

# Set the locale
RUN locale-gen de_DE.UTF-8
ENV LANG de_DE.UTF-8
ENV LANGUAGE de_DE.UTF-8
ENV LC_ALL de_DE.UTF-8

RUN mkdir -p /var/run/sshd

# Copy files into container
COPY docker-entrypoint.sh /usr/bin
COPY supervisord.conf /etc
COPY jail.local /etc/fail2ban
COPY 50-default.conf /etc/rsyslog.d
COPY rsyslog.conf /etc

ENTRYPOINT ["/usr/bin/docker-entrypoint.sh"]
