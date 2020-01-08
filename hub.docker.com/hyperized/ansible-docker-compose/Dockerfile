FROM hyperized/scratch:latest as trigger
# Used to trigger Docker hubs auto build, which it wont do on the official images

FROM hyperized/ansible-docker:2.8-bionic

LABEL maintainer="Gerben Geijteman <gerben@hyperized.net>"
LABEL description="Ubuntu Bionic with Ansible 2.8, cURL and Docker Compose"

RUN apt-get -y install curl && \
    curl -L "https://github.com/docker/compose/releases/download/1.24.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose && \
    chmod +x /usr/local/bin/docker-compose && \
    ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
