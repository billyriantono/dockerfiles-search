FROM clouder/clouder-base
MAINTAINER Yannick Buron yburon@goclouder.net

# create the odoo user
RUN adduser --home=/home/odoo --disabled-password --gecos "" --shell=/bin/bash odoo
RUN touch /home/odoo/.pgpass

RUN mkdir -p /opt/odoo/data
RUN mkdir -p /opt/odoo/etc
RUN mkdir -p /opt/odoo/extra-addons
RUN mkdir -p /opt/odoo/var/run
RUN mkdir -p /opt/odoo/var/log
RUN mkdir -p /opt/odoo/var/egg-cache
ADD sources/odoo.conf /opt/odoo/etc/odoo.conf

RUN chown -R odoo:odoo /opt/odoo

CMD tail -f /opt/odoo/etc/odoo.conf
