FROM ubuntu:16.04

# Update the apt-get
RUN apt-get update

# Install the ssh
RUN apt-get install openssh-server -y
RUN mkdir /var/run/sshd
RUN echo 'root:secret' | chpasswd
RUN sed -ri 's/^PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config

# Install the nginx
RUN apt-get install nginx -y

# Install the php and php-fpm
RUN apt-get install php php-fpm -y

# Start services
CMD /usr/sbin/sshd && service php7.0-fpm start && nginx

# Serve ports
EXPOSE 22 80