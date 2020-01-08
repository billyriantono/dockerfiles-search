FROM ubuntu:16.04

# Install "software-properties-common" (for the "add-apt-repository")
RUN apt-get update && apt-get install -y \
    software-properties-common \
    supervisor

# Install Mysql
RUN echo "mysql-server mysql-server/root_password password root" | debconf-set-selections \
    && echo "mysql-server mysql-server/root_password_again password root" | debconf-set-selections \
    && apt-get install -y mysql-server

COPY entrypoint.sh /scripts/entrypoint.sh
RUN chmod a+x /scripts/entrypoint.sh

EXPOSE 80 443 3000

ENTRYPOINT ["/scripts/entrypoint.sh"]
