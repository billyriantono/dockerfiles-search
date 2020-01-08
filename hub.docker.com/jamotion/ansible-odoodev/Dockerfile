FROM jamotion/ansible-odoo:8.0-20171009
MAINTAINER Renzo Meister <rm@jamotion.ch>

USER root

# Change owner of odoo to odoo for debugging and hacking
RUN chown -R odoo.odoo /usr/lib/python2.7/dist-packages/openerp

# Install and configure OpenSSH Server (for development mode only)
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get -y install openssh-server pwgen build-essential
RUN mkdir -p /var/run/sshd \
    && sed -i "s/UsePrivilegeSeparation.*/UsePrivilegeSeparation no/g" /etc/ssh/sshd_config \
    && sed -i "s/UsePAM.*/UsePAM no/g" /etc/ssh/sshd_config \
    && sed -i "s/PermitRootLogin.*/PermitRootLogin yes/g" /etc/ssh/sshd_config

# add special scripts for development
ADD bin /usr/local/bin

VOLUME ["/var/lib/odoo", "/etc/odoo", "/var/log/odoo"]

# Expose Odoo services
EXPOSE 8069 8072 22

# Set the default config file
ENV OPENERP_SERVER /etc/odoo/odoo-server.conf

ENTRYPOINT ["/usr/local/bin/run.sh"]
