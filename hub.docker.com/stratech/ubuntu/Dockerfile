#++++++++++++++++++++++++++++++++++++++
# stratech/ubuntu
#++++++++++++++++++++++++++++++++++++++
# Ubuntu BaseImage Docker container
#++++++++++++++++++++++++++++++++++++++
# Use phusion/baseimage as base image. To make your builds reproducible, make
# sure you lock down to a specific version, not to `latest`!
# See https://github.com/phusion/baseimage-docker/blob/master/Changelog.md for
# a list of version numbers.

FROM phusion/baseimage:0.9.18
MAINTAINER Stefano Mazzega <stefano.mazzega@gmail.com>

# Use the runit init system.
CMD ["/sbin/my_init"]


# Set TERM so that nano can work
ENV TERM=xterm

# Ensure OS is up-to-date
RUN apt-get update && apt-get upgrade -y -o Dpkg::Options::="--force-confold"

# Install utilities
RUN apt-get && apt-get install -y \
  curl \
  nano \
  wget \
  zip

#########################################
# Enable SSH
RUN rm -f /etc/service/sshd/down

# Regenerate SSH host keys. baseimage-docker does not contain any, so you
# have to do that yourself. You may also comment out this instruction; the
# init system will auto-generate one during boot.
RUN /etc/my_init.d/00_regen_ssh_host_keys.sh

# Enabling the insecure key permanently
RUN /usr/sbin/enable_insecure_key

# Login to the container
#ssh -i insecure_key root@<IP address>
# Running a command inside the container
#ssh -i insecure_key root@<IP address> echo hello world
#########################################



# Clean up APT when done.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
