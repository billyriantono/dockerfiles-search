FROM drieshooghe/directus-base:latest
LABEL maintainer "Dries Hooghe <dries@drieshooghe.com>"

RUN get-directus-api 2.0.0-rc.2
RUN fix-directus-api-permissions

COPY 000-default.conf /etc/apache2/sites-available

CMD ["run-directus-api"]