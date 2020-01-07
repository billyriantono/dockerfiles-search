FROM alpine:3.5

MAINTAINER Ron van der wijngaard <rvdwijngaard@to-increase.com>

ENV ENVCONSUL_VERSION 0.6.0

ENV SERVICE_6060_NAME profiling
ENV SERVICE_8081_NAME hystrix-stream

RUN \
  apk update && \
  apk add ca-certificates curl && \
  apk add wget tar && \
	wget -q --no-check-certificate -O /tmp/envconsul.zip https://releases.hashicorp.com/envconsul/${ENVCONSUL_VERSION}/envconsul_${ENVCONSUL_VERSION}_linux_amd64.zip && \
  unzip -d /tmp /tmp/envconsul.zip && \
  rm /tmp/envconsul.zip && \
  mv /tmp/envconsul /usr/bin && \
  apk del wget tar && \
  rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* *.gz && \
  rm -rf /var/cache/apk/*
ADD to-increase-init /bin/to-increase-init
ADD health-check-scheduler /bin/health-check-scheduler
ADD health-check /bin/health-check
ADD settings.profile /etc/settings.profile
ADD envconsul-config.hcl /etc/envconsul-config.hcl

EXPOSE 8080
EXPOSE 8081
EXPOSE 6060

ENTRYPOINT [ "/bin/to-increase-init" ]

CMD []
