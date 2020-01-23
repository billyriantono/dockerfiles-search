FROM ubuntu:16.04
ENV LANG='zh_CN.UTF-8'

RUN apt-get update \
    && apt-get install -y curl \
    && apt-get clean

ENV KIBANA_VERSION=6.3.2 \
    KIBANA_HOME=/kibana \
    PATH=${KIBANA_HOME}/bin:$PATH

WORKDIR ${KIBANA_HOME}

RUN  curl -fL https://artifacts.elastic.co/downloads/kibana/kibana-$KIBANA_VERSION-linux-x86_64.tar.gz \
    | tar --strip-components=1 -zx

COPY run.sh /
RUN chmod  775 /run.sh
CMD ["/run.sh"]
