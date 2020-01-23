# https://github.com/phusion/baseimage-docker
FROM phusion/baseimage

MAINTAINER dcolcott@cisco.com

# Add non-root user nso-user and make runit boot loader directories for NSO.
# At this stage add /etc/service/nso/down to prevent runit trying to start. 
RUN adduser --disabled-password --gecos "" nso-user
#mkdir -p /etc/service/nso && \
#mkdir -p /var/log/nso && \
#touch /etc/service/nso/down

ENV PUB_KEYPAIR=ssh-keys/nso-user-keypair.pub
ENV ROOT_PUB_KEYPAIR=ssh-keys/nso-root-keypair.pub

COPY $ROOT_PUB_KEYPAIR /root/.ssh/authorized_keys
COPY $PUB_KEYPAIR /home/nso-user/.ssh/authorized_keys

# Build layer with install tools / development binaries for fat nso-base container. 
RUN apt-get -y update && \
apt-get -y install software-properties-common build-essential ant python-software-properties git net-tools && \
apt-get remove -y openjdk-6-jre openjdk-6-jdk && \
apt-get remove -y openjdk-7-jre openjdk-7-jdk && \
add-apt-repository -y ppa:openjdk-r/ppa && \
apt-get update && apt-get install -y openjdk-8-jdk && \
apt-get -y autoremove && \
# For the phusion:baseimage to enable SSH
rm -f /etc/service/sshd/down && \
# final clean up of apt
apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
# change /home/nso/.ssh/authorized_keys owner to nso-user
chown nso-user:nso-user /home/nso-user/.ssh/authorized_keys

# Build layer with all NSO-ROSS packages saved from Git to /home/nso-user/nso-ross
# A symbolic link is copied into the NSO install in the parent container. 
# TBA...
 
EXPOSE 22

# The runit init script for phusion/baseimage
CMD ["/sbin/my_init"]

