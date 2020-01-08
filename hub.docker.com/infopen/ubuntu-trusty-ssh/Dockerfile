FROM ubuntu-upstart:trusty
MAINTAINER Alexandre Chaussier <a.chaussier@infopen.pro>

# Setting for packages installation
ENV DEBIAN_FRONTEND noninteractive

# Install openssh
RUN apt-get update && \
    apt-get install -y  openssh-server=1:6.6*

# TEst fix about 'Unable to connect to upstart'
RUN dpkg-divert --local --rename --add /sbin/initctl &&\
    ln -s /bin/true /sbin/initctl

# Setting the loginuid process attribute become optional
RUN sed -i 's/^(session\s+)required(\s+pam_loginuid.so)$/$1optional$2/g' \
    /etc/pam.d/sshd

# Ensure directory to store sshd pid exists
RUN mkdir -p /var/run/sshd

# Standard SSH port
EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]

