FROM atgjack/node 
MAINTAINER atgJack, https://github.com/atgJack/docker-alpine

# Set environment variables
ENV KIBANA_VERSION 4.6.1
ENV PKG_NAME kibana
ENV PKG_PLATFORM linux-x86_64
ENV KIBANA_PKG $PKG_NAME-$KIBANA_VERSION-$PKG_PLATFORM
ENV KIBANA_HOME /opt/$KIBANA_PKG/
ENV KIBANA_CONFIG $KIBANA_HOME/config/kibana.yml
ENV KIBANA_URL https://download.elastic.co/$PKG_NAME/$PKG_NAME/$KIBANA_PKG.tar.gz
ENV ELASTICSEARCH_HOST elasticsearch
ENV PATH=${PATH}:${KIBANA_HOME}/bin

# Download Kibana
RUN apk add --update curl bash \
    && mkdir -p /opt \
    && curl -o /tmp/$KIBANA_PKG.tar.gz $KIBANA_URL \
    && tar -xzf /tmp/$KIBANA_PKG.tar.gz -C /opt/ \
    && ln -s $KIBANA_HOME /opt/$PKG_NAME \
    && sed -i "s/localhost/$ELASTICSEARCH_HOST/" $KIBANA_CONFIG \
    && rm -rf /tmp/*.tar.gz /var/cache/apk/* /opt/$KIBANA_PKG/node/ \
    && mkdir -p $KIBANA_HOME/node/bin/ \
    && ln -s $(which node) /opt/$PKG_NAME/node/bin/node \
    && chmod o+w $KIBANA_HOME/optimize/.babelcache.json \
    && apk del curl

# Expose
EXPOSE 5601

USER nobody

# Working directory
WORKDIR ["/opt/kibana"]
CMD ["kibana", "-e", "http://elasticsearch:9200"]
