FROM debian:stretch

RUN set -ex && \
    apt-get update && \
    apt-get install -y --no-install-recommends \
		ca-certificates git mercurial subversion wget gettext \
		openjdk-8-jdk openjdk-8-jre-headless \
	&& \
    apt-get clean -y && \
    rm -rf /var/lib/apt/lists/*

ENV BAMBOO_VERSION=6.6.3 \
    BAMBOO_SCHEME=http \
    BAMBOO_PROXY_NAME= \
    BAMBOO_PROXY_PORT=

RUN set -ex && \
	addgroup bamboo && \
	useradd -d /bamboo -m -g bamboo bamboo && \
    wget -O - https://www.atlassian.com/software/bamboo/downloads/binary/atlassian-bamboo-${BAMBOO_VERSION}.tar.gz | tar -zx && \
	echo "bamboo.home = /bamboo" > /atlassian-bamboo-${BAMBOO_VERSION}/atlassian-bamboo/WEB-INF/classes/bamboo-init.properties && \
    chown -R bamboo:bamboo /bamboo /atlassian-bamboo-${BAMBOO_VERSION}/

USER bamboo

ADD server.xml.in /atlassian-bamboo-${BAMBOO_VERSION}/conf/server.xml.in

ADD bamboo.sh /

EXPOSE 8085 54663

CMD /bamboo.sh

