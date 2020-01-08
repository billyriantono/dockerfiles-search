FROM mysql:5.6

# Hack for boot2docker
#   see. https://github.com/boot2docker/boot2docker/issues/581

ENV UID 1000
RUN usermod -u "${UID}" mysql
RUN chown "${UID}" /var/run/mysqld

CMD ["mysqld"]
