FROM alpine:3.8 as builder

MAINTAINER yonfan.zhao <seltonzyf@gmail.com>

ENV FILEBEAT_VERSION=6.4.2 \
    FILEBEAT_SHA1=ee4e98fe5e3bfa31d40069912755a7396f7d570c973c6e9f7d0ff56f514db1cb15467cdaac17ef01f05fea1258bed3d511c569e0b716d44365fba2f9ebb42dd0

RUN set -x && \
  apk update && \
  apk add ca-certificates wget && \
  update-ca-certificates && \
  echo "start install filebeat." && \
  wget https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-${FILEBEAT_VERSION}-linux-x86_64.tar.gz -O /filebeat.tar.gz && \
  echo "${FILEBEAT_SHA1}  filebeat.tar.gz" | sha512sum -c -

FROM alpine:3.8 as final

WORKDIR /opt

COPY --from=builder /filebeat.tar.gz .

RUN set -x && \
  apk add libc6-compat && \
  tar xzvf filebeat.tar.gz && \
  cd filebeat-* && \
  cp filebeat /bin && \
  cd /opt && \
  rm -rf filebeat*
CMD [ "filebeat", "-e", "-c", "/filebeat.yml"]
