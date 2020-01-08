FROM node:6.9.0

# add our user and group first to make sure their IDs get assigned consistently
RUN groupadd -r kibana && useradd -r -m -g kibana kibana

RUN apt-get update && apt-get install -y \
                apt-transport-https \
                ca-certificates \
                wget \
# generating PDFs requires libfontconfig and libfreetype6
                libfontconfig \
                libfreetype6 \
        --no-install-recommends && rm -rf /var/lib/apt/lists/*

# grab gosu for easy step-down from root
ENV GOSU_VERSION 1.7
RUN set -x \
        && wget -O /usr/local/bin/gosu "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-$(dpkg --print-architecture)" \
        && wget -O /usr/local/bin/gosu.asc "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-$(dpkg --print-architecture).asc" \
        && export GNUPGHOME="$(mktemp -d)" \
        && gpg --keyserver ha.pool.sks-keyservers.net --recv-keys B42F6819007F00F88E364FD4036A9C25BF357DD4 \
        && gpg --batch --verify /usr/local/bin/gosu.asc /usr/local/bin/gosu \
        && rm -r "$GNUPGHOME" /usr/local/bin/gosu.asc \
        && chmod +x /usr/local/bin/gosu \
        && gosu nobody true

# grab tini for signal processing and zombie killing
ENV TINI_VERSION v0.9.0
RUN set -x \
        && wget -O /usr/local/bin/tini "https://github.com/krallin/tini/releases/download/$TINI_VERSION/tini" \
        && wget -O /usr/local/bin/tini.asc "https://github.com/krallin/tini/releases/download/$TINI_VERSION/tini.asc" \
        && export GNUPGHOME="$(mktemp -d)" \
        && gpg --keyserver ha.pool.sks-keyservers.net --recv-keys 6380DC428747F6C393FEACA59A84159D7001A4E5 \
        && gpg --batch --verify /usr/local/bin/tini.asc /usr/local/bin/tini \
        && rm -r "$GNUPGHOME" /usr/local/bin/tini.asc \
        && chmod +x /usr/local/bin/tini \
        && tini -h

RUN set -ex; \
# https://artifacts.elastic.co/GPG-KEY-elasticsearch
        key='46095ACC8548582C1A2699A9D27D666CD88E42B4'; \
        export GNUPGHOME="$(mktemp -d)"; \
        gpg --keyserver ha.pool.sks-keyservers.net --recv-keys "$key"; \
        gpg --export "$key" > /etc/apt/trusted.gpg.d/elastic.gpg; \
        rm -r "$GNUPGHOME"; \
        apt-key list

# install git
RUN set -x \
        && apt-get update \
        && apt-get install git -y \
        && git config --global user.name "Echolee" \
        && git config --global user.email 759768159@qq.com

# https://www.elastic.co/guide/en/kibana/5.0/deb.html
RUN echo 'deb https://artifacts.elastic.co/packages/5.x/apt stable main' > /etc/apt/sources.list.d/kibana.list

ENV KIBANA_VERSION 5.1.2

RUN set -x \
       && apt-get update \
       && apt-get install -y --no-install-recommends kibana=$KIBANA_VERSION \
       && rm -rf /var/lib/apt/lists/* \
        \
# the default "server.host" is "localhost" in 5+
        && sed -ri "s!^(\#\s*)?(server\.host:).*!\2 '0.0.0.0'!" /etc/kibana/kibana.yml \
        && grep -q "^server\.host: '0.0.0.0'\$" /etc/kibana/kibana.yml \
        \
# ensure the default configuration is useful when using --link
        && sed -ri "s!^(\#\s*)?(elasticsearch\.url:).*!\2 'http://elasticsearch:9200'!" /etc/kibana/kibana.yml \
        && grep -q "^elasticsearch\.url: 'http://elasticsearch:9200'\$" /etc/kibana/kibana.yml

RUN set -x \
	&& cd /usr \
	&& git clone https://github.com/Echolee-L/kibana.git -b 5.1.2-dev

# replace
RUN set -x \	
	&& rm -r /usr/share/kibana/src \
	&& cp -r -f /usr/kibana/src/ /usr/share/kibana/src \
	&& rm /usr/share/kibana/package.json \
	&& cp -f /usr/kibana/package.json /usr/share/kibana/ \
	&& rm -r /usr/kibana \
	&& rm -r /usr/share/kibana/node_modules \
	&& cd /usr/share/kibana \
	&& npm install

# install plugins
RUN set -x \
	&& cd /usr/share/kibana \
	&& bin/kibana-plugin install https://github.com/DeanF/health_metric_vis/releases/download/v0.3.5/health_metric_vis-5.1.2.zip \
	&& chown -R kibana:kibana /usr/share/kibana/optimize/ \
	&& cd /usr/share/kibana/plugins \
	&& git clone https://github.com/Echolee-L/kibana-relational-filter.git \
	&& git clone https://github.com/Echolee-L/kanban_vis.git \
	&& git clone https://github.com/Echolee-L/kbn_c3js_vis.git \
	&& cd kbn_c3js_vis \
	&& npm install

# clean
RUN set -x \
        && apt-get -y autoremove \
        && apt-get clean

ENV PATH /usr/share/kibana/bin:$PATH

COPY docker-entrypoint.sh /

EXPOSE 5601
ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["kibana"]
