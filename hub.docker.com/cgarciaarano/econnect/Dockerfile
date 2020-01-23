FROM odoo:11.0

USER root

RUN curl -L https://github.com/schneidexe/tpl/releases/download/v0.4.4/tpl-linux-amd64 -o /bin/tpl
# RUN apt update && install libldap2-dev libsasl2-dev
# RUN pip3 install vobject qrcode pyldap

COPY ./odoo.conf.tpl /etc/odoo/
COPY ./entrypoint.sh /

USER odoo