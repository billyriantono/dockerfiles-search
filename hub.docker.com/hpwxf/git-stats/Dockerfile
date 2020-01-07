FROM debian:stretch-slim

MAINTAINER Pascal Havé <hpwxf@haveneer.com>
ENV REFRESHED_AT 2019-12-08

RUN useradd -u 950 -U -s /bin/false -M -r -G users docker

# Supervisor utility (cf http://supervisord.org)
RUN apt-get update \
    && apt-get install -y python-pip \
    && pip install supervisor \
    && apt-get autoremove --purge -y && apt-get clean && rm -rf /var/lib/apt/lists/*

RUN mkdir /tmp/sockets
COPY etc/supervisord.conf /etc

# git-stats installation (cf https://github.com/tomgi/git_stats)
RUN apt-get update \
    && apt-get install -y ruby ruby-nokogiri ruby-nokogiri-diff ruby-nokogumbo \
    && gem install git_stats \
    && apt-get autoremove --purge -y && apt-get clean && rm -rf /var/lib/apt/lists/*

# Nginx and git tools
RUN apt-get update \
    && apt-get install -y nginx git \
    && apt-get autoremove --purge -y && apt-get clean && rm -rf /var/lib/apt/lists/*
RUN useradd -U -s /bin/false -M -r nginx

# Add custom scripts
COPY generatord.sh /
COPY nginx.conf /etc/nginx/conf.d/git-stats.conf
COPY init/ /init/
COPY hooks/ /hooks/
COPY supervisord.d/ /etc/supervisord.d/

RUN chmod +x /generatord.sh

ENTRYPOINT ["/bin/bash", "-e", "/init/entrypoint"]
CMD ["run"]

VOLUME ["/data"]
EXPOSE 8080
