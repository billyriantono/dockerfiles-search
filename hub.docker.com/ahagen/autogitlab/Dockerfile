FROM gitlab/gitlab-ce

RUN apt-get update
RUN apt-get --yes dist-upgrade

RUN apt-get --yes install letsencrypt
RUN apt-get --yes install cron
RUN apt-get --yes install python3

COPY init.sh /usr/local/bin/init_gitlab
RUN chmod +x /usr/local/bin/init_gitlab

SHELL ["/bin/sh", "-c"]
CMD init_gitlab