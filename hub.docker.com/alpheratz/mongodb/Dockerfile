
FROM phusion/baseimage:0.9.11

MAINTAINER Maxim Dubrovin <maxxdubrovin@gmail.com>

# baseimage:

# Set correct environment variables.
ENV HOME /root

# Regenerate SSH host keys. baseimage-docker does not contain any, so you
# have to do that yourself. You may also comment out this instruction; the
# init system will auto-generate one during boot.
# RUN /etc/my_init.d/00_regen_ssh_host_keys.sh

# Use baseimage init system.
CMD ["/sbin/my_init"]



# me:

# Disable baseimage SSH
RUN rm -rf /etc/service/sshd /etc/my_init.d/00_regen_ssh_host_keys.sh

# Start MongoDB Installation:
# build context (for ADD): private bitbucket repo

# Import MongoDB public GPG key AND create a MongoDB list file
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10
RUN echo 'deb http://downloads-distro.mongodb.org/repo/ubuntu-upstart dist 10gen' | tee /etc/apt/sources.list.d/10gen.list

# Update apt-get sources AND install MongoDB:2.6.4
RUN apt-get update && apt-get install -y mongodb-org=2.6.4 mongodb-org-server=2.6.4 mongodb-org-shell=2.6.4 mongodb-org-mongos=2.6.4 mongodb-org-tools=2.6.4

# mongod runit script (runit unitl goes with baseimage)
# will automatically start/restart mongod
# service with mongodb.conf on ubuntu start
# (no need ENTRYPOINT)
# Create directory for mongod runit script
RUN mkdir -p /etc/service/mongod

# add script from run.sh
# to /etc/service/mongod/run script
ADD /run.sh /etc/service/mongod/run

# Make run script executable
RUN chmod +x /etc/service/mongod/run

# add mongodb config
# ADD /mongodb.conf /data/

EXPOSE 27017

# baseimage: Clean up APT when done.

RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

