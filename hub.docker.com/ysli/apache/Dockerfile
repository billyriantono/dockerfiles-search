FROM httpd:alpine
COPY httpd.conf conf
COPY httpd-dav.conf conf/extra
RUN mkdir var; \
    chown daemon:www-data var htdocs
