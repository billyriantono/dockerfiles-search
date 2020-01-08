FROM debian:stable-slim

WORKDIR /root

RUN apt-get update && apt-get install wget -y && apt-get clean && \
    wget https://dl.google.com/cloudsql/cloud_sql_proxy.linux.amd64 && \
    mv cloud_sql_proxy.linux.amd64 cloud_sql_proxy && \
    chmod +x cloud_sql_proxy

CMD ./cloud_sql_proxy -instances=${INSTANCE_CONNECTION_NAME}=tcp:0.0.0.0:3306 -credential_file=./credential