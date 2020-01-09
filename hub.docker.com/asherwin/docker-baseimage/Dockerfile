#
# Base Image for local development
#

FROM phusion/baseimage:0.9.11
MAINTAINER Alex Sherwin <alex.sherwin@gmail.com>

ENV HOME /root

RUN rm -rf /etc/service/sshd /etc/my_init.d/00_regen_ssh_host_keys.sh

CMD ["/sbin/my_init"]
