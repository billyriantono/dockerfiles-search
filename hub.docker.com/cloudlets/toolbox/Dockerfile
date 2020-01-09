FROM ubuntu:18.04

RUN apt-get update

# Configure SSH
RUN apt-get install -y openssh-server
RUN mkdir /var/run/sshd

RUN mkdir /root/.ssh

EXPOSE 22

# Setup handy development packages
RUN apt install -y vim git curl wget

# Cowsay welcome message
RUN apt-get install -y cowsay
COPY docker.cow /usr/share/cowsay/cows/docker.cow
RUN rm -r /etc/update-motd.d/*
COPY ./sshd /etc/pam.d/sshd

# Clean apt-get
RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Add cloudlets user
RUN useradd -ms /bin/bash cloudlets
RUN usermod -a -G www-data cloudlets

# Setup custom .bashrc
COPY .bashrc /home/cloudlets/.bashrc

# Install useful development packages
ARG DEBIAN_FRONTEND=noninteractive
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash -
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN apt update && apt install -y nodejs php7.2-cli composer redis-tools mysql-client yarn
RUN curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar
RUN chmod +x wp-cli.phar
RUN mv wp-cli.phar /usr/local/bin/wp

CMD ["/usr/sbin/sshd", "-D"]