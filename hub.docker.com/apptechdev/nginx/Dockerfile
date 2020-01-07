FROM nginx

RUN rm -rf /etc/nginx/conf.d/* && \
    mkdir -p /etc/nginx/sites-enabled && \
    mkdir -p /etc/nginx/sites-available

COPY ./nginx /etc/nginx

RUN ln -s /etc/nginx/sites-available/default.conf /etc/nginx/sites-enabled/default.conf
