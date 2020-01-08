FROM ubuntu:xenial
MAINTAINER Pascal Martineau <pascal@lewebsimple.ca>

# Install package dependencies
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
  ca-certificates \
  less \
  iputils-ping \
  mysql-server \
  nano \
  supervisor \
  && rm -rf /var/lib/apt/lists/*

# Default MySQL UID
ENV MYSQL_UID 1000

# Copy configuration files
COPY config/ /

# Configure MySQL
RUN set -ex \

  # Create empty data directory
  && rm -rf /var/lib/mysql \
  && mkdir -p /var/lib/mysql /var/run/mysqld \

  # Change UID/GID of mysql to match local user
  && usermod --non-unique --uid ${MYSQL_UID} mysql \
  && groupmod --non-unique --gid ${MYSQL_UID} mysql \

  # Adjust directory ownership and permissions
  && chown -R mysql:mysql /var/lib/mysql /var/run/mysqld \
  && chmod 777 /var/run/mysqld \

  # Adjust MySQL configuration (bind-address, log)
  && sed -Ei 's/^(bind-address|log)/#&/' /etc/mysql/mysql.conf.d/mysqld.cnf

VOLUME ["/var/lib/mysql"]

EXPOSE 3306

CMD ["/docker-entrypoint.sh"]
