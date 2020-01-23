FROM haproxy:1.6.13

ENV AMDATU_HAPROXY_REST_VERSION=1.4.2
ENV CONFD_VERSION 0.11.0

ADD bootstrap-confd-haproxy.sh /bootstrap-confd-haproxy.sh
ADD haproxy.toml /etc/confd/conf.d/haproxy.toml
ADD haproxy.tmpl /etc/confd/templates/haproxy.tmpl
ADD reload_haproxy.sh /reload_haproxy.sh
ADD https://bitbucket.org/amdatulabs/amdatu-haproxy-rest/downloads/amdatu-haproxy-rest-linux_amd64-${AMDATU_HAPROXY_REST_VERSION} /usr/local/bin/amdatu-haproxy-rest

ADD https://github.com/kelseyhightower/confd/releases/download/v${CONFD_VERSION}/confd-${CONFD_VERSION}-linux-amd64 /usr/local/bin/confd
RUN chmod +x /usr/local/bin/confd && mkdir /etc/haproxy && chmod +x /bootstrap-confd-haproxy.sh && chmod +x /reload_haproxy.sh && chmod +x /usr/local/bin/amdatu-haproxy-rest
RUN apt-get update && apt-get install socat -y

EXPOSE 80 443 1936 5000 8080 8787

VOLUME /etc/ssl/private/

CMD /bootstrap-confd-haproxy.sh
