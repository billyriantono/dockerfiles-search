
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

# Start HAproxy install:
# build context (for ADD): private bitbucket repo

RUN add-apt-repository ppa:vbernat/haproxy-1.5 && apt-get update

RUN apt-get install haproxy

RUN mkdir -p /etc/service/haproxy

ADD /run.sh /etc/service/haproxy/run

RUN chmod +x /etc/service/haproxy/run

EXPOSE 80
EXPOSE 433

# baseimage: Clean up APT when done.

RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

