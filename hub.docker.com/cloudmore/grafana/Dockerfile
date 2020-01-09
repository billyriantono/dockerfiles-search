FROM alpine:3.5

EXPOSE 3000

ARG APK_CACHE_IP=172.17.0.1
ARG APK_CACHE_DOMAIN='dl-cdn.alpinelinux.org'

ARG RUN_DEPS=''
ARG BUILD_DEPS='openssl coreutils tar g++ go git mercurial make nodejs'

ARG GOPATH=/tmp
ARG GOPKG=/usr/lib/go/pkg

#ARG GRAFANA_VERSION=4.0.2
ARG GRAFANA_TAGS='https://api.github.com/repos/grafana/grafana/tags'
ARG GRAFANA_URL='https://github.com/grafana/grafana/archive'

ARG REPO=github.com/grafana/grafana
ENV GRAFANA_TMP=$GOPATH/src/$REPO
ENV GRAFANA_HOME=/opt/grafana

RUN nc -z $APK_CACHE_IP 80 && echo $APK_CACHE_IP $APK_CACHE_DOMAIN >>/etc/hosts \
 ; apk --update add --no-cache $RUN_DEPS $BUILD_DEPS \
   && mkdir -p $GRAFANA_TMP && cd $GRAFANA_TMP \
   && GRAFANA_LATEST=$(wget -qO- $GRAFANA_TAGS | egrep -o "[0-9]+\.[0-9]+\.[0-9]+\"" | sort -Vr | head -1 | tr -d '"') \
   && wget -O- $GRAFANA_URL/v${GRAFANA_VERSION:=$GRAFANA_LATEST}.tar.gz | tar xz --strip-components=1 \
   && go run build.go setup \
   && go run build.go build \
   && npm install \
   && npm install -g grunt-cli \
   && grunt \
   && mkdir -p $GRAFANA_HOME/data \
   && mv -v $GRAFANA_TMP/bin $GRAFANA_TMP/conf $GRAFANA_HOME \
   && mv $GRAFANA_TMP/public_gen $GRAFANA_HOME/public \
   && $GRAFANA_HOME/bin/grafana-cli --pluginsDir $GRAFANA_HOME/public/plugins plugins install grafana-kairosdb-datasource \
 && apk del $BUILD_DEPS && rm -rf /var/cache/apk/* $GOPATH $GOPKG /root/.npm /root/.node-gyp

WORKDIR $GRAFANA_HOME

VOLUME $GRAFANA_HOME/data

CMD ["./bin/grafana-server"]
