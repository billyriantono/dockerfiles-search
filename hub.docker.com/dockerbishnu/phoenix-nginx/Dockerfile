FROM nginx:stable

RUN apt-get update -y \
    && apt-get install -y --no-install-recommends \
        bc \
        curl \
        unzip \
        vim  \
    && rm -rf /var/lib/apt/lists/*

ADD ./conf.d /etc/nginx/conf.d
