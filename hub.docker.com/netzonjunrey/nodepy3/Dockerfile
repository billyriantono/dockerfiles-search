# docker build --rm -f Dockerfile -t netzon-docker-phusion-dotnet-core:latest .
# Use phusion/baseimage as base image. To make your builds reproducible, make
# sure you lock down to a specific version, not to `latest`!
# See https://github.com/phusion/baseimage-docker/blob/master/Changelog.md for
# a list of version numbers.
FROM phusion/baseimage:0.10.1

# Use baseimage-docker's init system.
CMD ["/sbin/my_init"]

# Install all other apps
RUN AZ_REPO=$(lsb_release -cs) \
    && echo "deb http://ppa.launchpad.net/ansible/ansible/ubuntu trusty main" >> /etc/apt/sources.list \
    && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367 \
    && curl -sL https://deb.nodesource.com/setup_8.x | bash - \
    && apt-get -y update

RUN apt-get -y install nodejs
RUN apt-get -y install ansible
RUN apt-get -y install python3-venv
RUN apt-get -y install python3-pip
RUN npm install -g @angular/cli@1.6.5

# Clean up APT when done.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*