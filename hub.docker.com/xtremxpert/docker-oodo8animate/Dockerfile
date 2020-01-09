FROM odoo:8.0

MAINTAINER Benoît "XtremXpert" Vézina <xtremxpert@xtremxpert.com>

USER root

RUN apt-get update
RUN apt-get install -y curl
RUN curl -sL https://deb.nodesource.com/setup_4.x | bash -
RUN apt-get install -y nodejs
RUN npm install -g less less-plugin-clean-css

USER odoo

ENTRYPOINT ["/entrypoint.sh"]
CMD ["openerp-server"]
