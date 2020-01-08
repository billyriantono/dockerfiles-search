FROM minio/mc:RELEASE.2019-12-24T23-41-36Z

ADD jq/* /jq/
ADD bin/* /bin/

RUN apk add --no-cache jq bash && \
  chmod +x /bin/*

WORKDIR /root