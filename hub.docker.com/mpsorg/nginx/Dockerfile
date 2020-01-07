FROM nginx:1.13

# Replace default access logging with JSON one
COPY config/json-access-log.conf /etc/nginx/conf.d/json-access-log.conf
RUN sed -i 's/\baccess_log\b.*\bmain;//g' /etc/nginx/nginx.conf

# Install root certificates
RUN set -x && \
    apt-get update && \
    apt-get install -y ca-certificates && \
    rm -r /var/lib/apt/lists/*

# Install aws-env
ARG AWS_ENV_VERSION=f6b72b9a61602f60b161590516dac2226e0cf197
ADD https://github.com/Droplr/aws-env/raw/${AWS_ENV_VERSION}/bin/aws-env-linux-amd64 /usr/local/bin/aws-env
RUN chmod +x /usr/local/bin/aws-env

# Install dockerize
ARG DOCKERIZE_VERSION=v0.5.0
ADD https://github.com/jwilder/dockerize/releases/download/${DOCKERIZE_VERSION}/dockerize-linux-amd64-${DOCKERIZE_VERSION}.tar.gz /dockerize.tar.gz
RUN set -x && \
    tar -C /usr/local/bin -xzvf /dockerize.tar.gz && \
    rm /dockerize.tar.gz
