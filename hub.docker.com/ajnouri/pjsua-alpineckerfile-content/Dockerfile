FROM openjdk:12-alpine

LABEL maintainer "ajacker <ajacker@foxmail.com>"

ENV VERSION=v13.1.0 NPM_VERSION=6 YARN_VERSION=latest

# For base builds
# ENV CONFIG_FLAGS="--fully-static --without-npm" DEL_PKGS="libstdc++" RM_DIRS=/usr/include

ARG ek_version=7.4.2

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g' /etc/apk/repositories \
&& apk add --no-cache nss bash \ 
&& adduser -D elasticsearch

USER elasticsearch

WORKDIR /home/elasticsearch

# ENV PATH /home/elasticsearch/node/bin:$PATH

ENV ES_TMPDIR=/home/elasticsearch/elasticsearch.tmp \
    ES_DATADIR=/home/elasticsearch/elasticsearch/data \
    JAVA_HOME=/opt/openjdk-12
    
RUN wget -q -O - https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-oss-${ek_version}-linux-x86_64.tar.gz \
 |  tar -zx \ 
 && mv elasticsearch-${ek_version} elasticsearch \
 && mkdir -p ${ES_TMPDIR} ${ES_DATADIR}

# https://github.com/medcl/elasticsearch-analysis-ik/releases
RUN echo -e "y" | sh elasticsearch/bin/elasticsearch-plugin install -s https://github.com/medcl/elasticsearch-analysis-ik/releases/download/v${ek_version}/elasticsearch-analysis-ik-${ek_version}.zip

CMD sh elasticsearch/bin/elasticsearch -E http.host=0.0.0.0

EXPOSE 9200