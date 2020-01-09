FROM odoo:8.0
MAINTAINER med@microcom.ca

USER root

# Installing dependance
RUN echo 'deb http://packages.linuxmint.com debian import' >> /etc/apt/sources.list \
    && apt-get update \
    && apt-get install -y --force-yes freetds-dev xvfb firefox python-pip python-dev\
    && pip install selenium==2.45.0 num2words pysftp plivo pymssql xvfbwrapper

#Creating volder for config, addons and logs
RUN /bin/bash -c "mkdir -p /opt/odoo/{bin,etc,sources/odoo,additional_addons,data/filestore}" && \
    /bin/bash -c "mkdir -p /opt/odoo/var/{run,log,egg-cache}" && \
    /bin/bash -c "cp -r /var/lib/odoo /opt/odoo/data/" && \
    /bin/bash -c "chmod -R 777 /opt/odoo/data"

# Mount /opt/odoo/data/filestore to allow restoring filestore, /opt/odoo/additional_addons for users addons and /opt/odoo/etc for config file
VOLUME ["/opt/odoo/data/filestore", "/opt/odoo/additional_addons", "/opt/odoo/etc"]

# Expose Odoo services
EXPOSE 8069 8071

# Set default user when running the container
USER odoo

ENTRYPOINT ["/entrypoint.sh"]
CMD ["openerp-server", "-c",  "/opt/odoo/etc/odoo.conf"]

