FROM nginx:alpine

RUN sed -i '/http {/a ssi on;' /etc/nginx/nginx.conf \
    && ln -s /etc/hostname /usr/share/nginx/html/hostname

COPY site /usr/share/nginx/html
