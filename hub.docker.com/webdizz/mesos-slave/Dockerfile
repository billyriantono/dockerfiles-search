FROM webdizz/mesos

MAINTAINER Izzet Mustafaiev "izzet@mustafaiev.com"

# Set correct environment variables.
ENV     HOME /root

RUN /etc/my_init.d/00_regen_ssh_host_keys.sh

# Use baseimage-docker's init system.
CMD ["/sbin/my_init"]

RUN mkdir -p /etc/service/mesos
ADD mesos-slave.sh /etc/service/mesos/run

USER root
EXPOSE 5051
