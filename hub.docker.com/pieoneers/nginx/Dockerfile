FROM nginx

ENV CONSUL_TEMPLATE_VERSION 0.14.0
ENV CONSUL_TEMPLATE_SHA256 7c70ea5f230a70c809333e75fdcff2f6f1e838f29cfb872e1420a63cdf7f3a78
ENV CONSUL_TEMPLATE_PACKAGE consul-template_${CONSUL_TEMPLATE_VERSION}_linux_amd64.zip

RUN \
  apt-get update &&\
  apt-get install -y unzip


WORKDIR /tmp

ADD https://releases.hashicorp.com/consul-template/${CONSUL_TEMPLATE_VERSION}/${CONSUL_TEMPLATE_PACKAGE} ${CONSUL_TEMPLATE_PACKAGE}

RUN \
  echo "${CONSUL_TEMPLATE_SHA256}  ${CONSUL_TEMPLATE_PACKAGE}" > CONSUL_TEMPLATE_SHA256SUM &&\
  sha256sum --check CONSUL_TEMPLATE_SHA256SUM &&\
  unzip ${CONSUL_TEMPLATE_PACKAGE} -d /usr/local/bin &&\
  chmod +x /usr/local/bin/consul-template

RUN rm -r *



WORKDIR /etc

RUN mkdir -p consul-template/{conf.d,templates}

WORKDIR /etc/nginx

ADD nginx.conf .
RUN rm conf.d/*


ADD docker-entrypoint.sh /

ENTRYPOINT ["/docker-entrypoint.sh"]
