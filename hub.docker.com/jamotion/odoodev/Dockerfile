FROM jamotion/odoo:8.0-20170201
MAINTAINER Renzo Meister <rm@jamotion.ch>

USER root

RUN chown -R odoo.odoo /usr/lib/python2.7/dist-packages/openerp

# Install and configure OpenSSH Server (for development mode only)
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get -y install openssh-server pwgen build-essential
RUN mkdir -p /var/run/sshd \
    && sed -i "s/UsePrivilegeSeparation.*/UsePrivilegeSeparation no/g" /etc/ssh/sshd_config \
    && sed -i "s/UsePAM.*/UsePAM no/g" /etc/ssh/sshd_config \
    && sed -i "s/PermitRootLogin.*/PermitRootLogin yes/g" /etc/ssh/sshd_config

ADD bin /opt/odoo/bin

ENV AUTHORIZED_KEYS **None**
VOLUME ["/opt/odoo/data", "/usr/local/share/fonts", "/etc/odoo", "/var/log/odoo"]

# Expose Odoo services
EXPOSE 22 8069 8071 8072

# Set the default config file
ENV OPENERP_SERVER /etc/odoo/odoo-server.conf

ENTRYPOINT ["/opt/odoo/bin/run.sh"]
