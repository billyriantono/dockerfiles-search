FROM ubuntu:latest
MAINTAINER palaphon@iknowplus.co.th;

WORKDIR /cloudctl/

RUN apt-get update && apt-get install -y curl sudo

ENV ICP_ENDPOINT=https://10.0.123.201:8443
ENV PATH="$PATH:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"

COPY run.sh /cloudctl/run.sh
RUN chmod +x /cloudctl/run.sh

