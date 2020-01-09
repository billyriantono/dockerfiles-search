FROM nginx:1.14-alpine

RUN echo "127.0.0.1	backend" >> /etc/hosts && echo "127.0.0.1 tigase" >> /etc/hosts

RUN mkdir -p /var/cache/nginx

COPY conf/* /etc/nginx/conf.d/

COPY  entrypoint.sh /usr/bin

# Volume for SSL certificate
VOLUME ["/www/cert"]

# This volume is from mercury image
VOLUME ["/www/mercury"]

# These volumes are from site image
VOLUME ["/www/media"]
VOLUME ["/www/static"]

CMD /usr/bin/entrypoint.sh
