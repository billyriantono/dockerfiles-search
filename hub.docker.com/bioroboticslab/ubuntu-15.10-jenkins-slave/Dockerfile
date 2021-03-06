# This Dockerfile is used to build an image containing basic stuff to be used as a Jenkins slave build node.

FROM ubuntu:15.04
MAINTAINER Michael Wittig <michael.wittig@fu-berlin.de>

#RUN sed -i 's/^mesg n$/tty -s \&\& mesg n/g' /root/.profile
ENV DEBIAN_FRONTEND noninteractive

# Make sure the package repository is up to date. RUN apt-get update
RUN apt-get -y update \
 && apt-get -y upgrade \

# Install a basic SSH server
 && apt-get install -y openssh-server \
 && sed -i 's|session    required     pam_loginuid.so|session    optional     pam_loginuid.so|g' /etc/pam.d/sshd \
 && mkdir -p /var/run/sshd \

# Install JDK 7 (latest edition)
# && apt-get install -y --force-yes tzdata=2015c-1
 && apt-get install -y openjdk-7-jdk \

# Add user jenkins to the image, use the some arbitrary high uid and gid to
# circumvent any clashes with host users
 && useradd --uid 4000 --gid 4000 -m jenkins \

# Set random passwords for the root and jenkins users.
 && echo "root:$(< /dev/urandom tr -dc A-Za-z0-9 | head -c 32)" | chpasswd \
 && echo "jenkins:$(< /dev/urandom tr -dc A-Za-z0-9 | head -c 32)" | chpasswd \

# Add jenkins SSH pubkey to authorized_keys
 && mkdir -p /home/jenkins/.ssh \

 && echo "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC/4M6G+wnzZFaxio8EVRhKXz/RMa1e0hh2eZeE5Da4S9pQnR7zcZNa90bpqHA9GOUfrYMoLOYXoQp5iKq/WzTzhQmVe6mxxuJMUWCQC1Ne2BMB3OkYjGeOeM4bRzFbM1SVxYAumoncdRB/77FN6D1EYgBWTr0ySRQOy3AbH5wMSb2ZKnhrd4W5JMqAxqyrSCoFUlXzD9gMeHzFhOoUItMh62U6CYPAErRDLPaFqjVOR9thzpfYl5xQ3xrS0ldmY8wL3u7mtMHG5wPt2xV4mfyHUqGlONpBKINPH4qKtJ3qsxdyaR0tvxCy8cbEEJLnfJFQcOg88E9X6M2NWVdNks/v jenkins@flip" >> /home/jenkins/.ssh/authorized_keys

# Start sshd and export Standard SSH port
EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
