FROM ubuntu:trusty
MAINTAINER Renzo Meister <rm@jamotion.ch>

# Install some deps, lessc and less-plugin-clean-css, and wkhtmltopdf
RUN apt-get update 
RUN apt-get install -y --no-install-recommends \
    ca-certificates 

# Install and configure OpenSSH Server (for development mode only)
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get -y install openssh-server pwgen
RUN mkdir -p /var/run/sshd \
    && sed -i "s/UsePrivilegeSeparation.*/UsePrivilegeSeparation no/g" /etc/ssh/sshd_config \
    && sed -i "s/UsePAM.*/UsePAM no/g" /etc/ssh/sshd_config \
    && sed -i "s/PermitRootLogin.*/PermitRootLogin yes/g" /etc/ssh/sshd_config

ADD bin /opt/odoo/bin

ENV AUTHORIZED_KEYS **None**

# Expose Odoo services
EXPOSE 22

ENTRYPOINT ["/opt/odoo/bin/run.sh"]
