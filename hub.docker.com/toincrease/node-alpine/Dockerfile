FROM mhart/alpine-node
 
MAINTAINER to-increase <to-increase.io>

RUN \
  apk update && \
  apk add wget tar && \
  wget -q --no-check-certificate -O /tmp/consul.tar.gz https://github.com/hashicorp/envconsul/releases/download/v0.5.0/envconsul_0.5.0_linux_amd64.tar.gz && \
  tar -xzvf /tmp/consul.tar.gz -C /usr/bin/ --strip-components=1 && \
  apk del wget tar && \
  rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* *.gz

ADD envconsul-config.hcl /etc/envconsul-config.hcl
ADD envconsul-launch /usr/bin/envconsul-launch

RUN chmod +x /usr/bin/envconsul-launch

ENTRYPOINT ["envconsul-launch"]
