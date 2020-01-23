FROM adhoc/odoo-ar:9.0

COPY ./requeriments.txt /tmp/requeriments.txt

USER root

RUN pip install -r /tmp/requeriments.txt

USER odoo
