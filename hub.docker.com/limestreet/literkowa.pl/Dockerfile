FROM nginx:stable

COPY ./html /usr/share/nginx/html

RUN chown www-data:www-data -R /usr/share/nginx/html \
    && find /usr/share/nginx/html/* -type d -print0 | xargs -0 chmod 0555 \
    && find /usr/share/nginx/html/ -type f -print0 | xargs -0 chmod 0444
