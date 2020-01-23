FROM python:3.5

RUN curl -sfSL 'https://get.docker.com/builds/Linux/x86_64/docker-1.12.1.tgz' -o docker.tgz \
        && tar -xzf docker.tgz \
        && mv docker/* /usr/local/bin/ \
        && rmdir docker \
        && rm docker.tgz \
        && docker -v \
        && pip install docker-compose

