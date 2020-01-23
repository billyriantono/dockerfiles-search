FROM centos:latest

# Metadata
LABEL mantainer="Gius. Camerlingo <gcamerli@gmail.com>"
LABEL version="1.0"
LABEL description="SMTP server for spixel."

# Docker image name
ENV NAME=smtp

# Timezone
ENV TZ="Europe/Paris"

# Update system packages
RUN yum install -y epel-release && yum update -y \
RUN yum install -y \
	cyrus-sasl \
	cyrus-sasl-plain \
	cyrus-sasl-md5 mailx \
	perl \
	supervisor \
	postfix \
	rsyslog

# Clean cache
RUN rm -rf /var/cache/yum/* \
	&& yum clean all

# Config supervisor and postfix
#RUN sed -i -e "s/^nodaemon=false/nodaemon=true/" /etc/supervisord.conf
#RUN sed -i -e 's/inet_interfaces = localhost/inet_interfaces = all/g' /etc/postfix/main.cf

# Copy config files
COPY etc/*.conf /etc/
COPY etc/rsyslog.d/* /etc/rsyslog.d
COPY run.sh /
RUN chmod +x /run.sh
COPY etc/supervisord.d/*.ini /etc/supervisord.d/
#RUN newaliases

# Port
EXPOSE 25

# Healthcheck
COPY healthcheck /usr/local/bin/
RUN chmod 744 /usr/local/bin/healthcheck

# User
RUN useradd -ms /bin/bash docker

# Home
ENV HOME=/home/docker

# Permissions
RUN chown -R docker:docker $HOME

# Change user
USER docker

# Command entrypoint
CMD ["/run.sh"]
