FROM php:7.2-cli

# Install PHP and composer dependencies
RUN apt-get update && apt-get install -yq git \
curl \
nodejs \
openssh-server \
mariadb-client \
unzip \
nano \
wget; \
mkdir -p /var/run/sshd; \
mkdir /root/.ssh && chmod 700 /root/.ssh; \
touch /root/.ssh/authorized_keys

# Clear out the local repository of retrieved package files
RUN apt-get clean

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
