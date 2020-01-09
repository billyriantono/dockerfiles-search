FROM httpd:2.4

MAINTAINER Jean Pommier "jean.pommier@pi-geosolutions.fr"

COPY ./sviewer/ /usr/local/apache2/htdocs/sviewer/
COPY ./config/customConfig.js /usr/local/apache2/htdocs/etc/customConfig.js

ENV DOMAIN_NAME "https://go.sk.pigeosolutions.fr"
ENV INITIAL_EXTENT "1900000,6000000,2500000,6500000"
ENV MAX_EXTENT "-20037508.34, -20037508.34, 20037508.34, 20037508.34"
ENV RESTRICTED_EXTENT "-20037508.34, -20037508.34, 20037508.34, 20037508.34"
ENV MAX_FEATURES 10

ADD entrypoint.sh /entrypoint.sh
RUN chmod u+x /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]

CMD ["httpd-foreground"]
