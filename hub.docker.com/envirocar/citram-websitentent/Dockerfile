FROM docker
RUN apk update && \ 
    apk add --no-cache py-pip python-dev libffi-dev openssl-dev gcc curl libc-dev make && \
    curl -L "https://github.com/docker/compose/releases/download/1.24.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose && \
    chmod +x /usr/local/bin/docker-compose
CMD sh
