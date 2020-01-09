FROM chiaen/docker-gcsfuse:latest

RUN apk add --update --no-cache openssl \
    && wget -q https://dl.google.com/cloudsql/cloud_sql_proxy.linux.amd64 \
    && mv cloud_sql_proxy.linux.amd64 cloud_sql_proxy \
    && chmod +x cloud_sql_proxy \
    && mkdir -p /cloudsql \
    && mv cloud_sql_proxy /usr/local/bin \
    && rm -rf /var/cache/apk
