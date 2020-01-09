FROM docker
MAINTAINER herve leclerc <herve.leclerc@alterway.fr>

RUN apk add --update python python-dev py-pip \
 && pip install docker-compose \
 && wget -O envconsul.zip https://releases.hashicorp.com/envconsul/0.6.1/envconsul_0.6.1_linux_amd64.zip \
 && unzip envconsul.zip \
 && mv envconsul /usr/local/bin \
 && rm -rf envconsul.zip \
 && rm -rf /var/cache/apk/*

ADD envconsul-config.hcl /etc/envconsul-config.hcl
ADD envconsul-launch /usr/local/bin/envconsul-launch

RUN chmod +x /usr/local/bin/envconsul-launch /usr/local/bin/envconsul

ENTRYPOINT ["/usr/local/bin/envconsul-launch"]
