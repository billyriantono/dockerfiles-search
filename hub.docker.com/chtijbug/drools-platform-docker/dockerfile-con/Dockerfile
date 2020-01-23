FROM ruby:2.4.1-stretch

# add our user and group first to make sure their IDs get assigned consistently, regardless of whatever dependencies get added
RUN echo "deb http://ftp.debian.org/debian jessie-backports main" | tee "/etc/apt/sources.list.d/jesse-backports.list"
RUN apt-get update \
	&& apt-get install -y --no-install-recommends \
		ca-certificates	\
		jq \
		numactl \
		libssl1.0.0 \
		awscli \
	&& rm -rf /var/lib/apt/lists/*

ENV GPG_KEYS \
# pub   4096R/AAB2461C 2014-02-25 [expires: 2016-02-25]
#       Key fingerprint = DFFA 3DCF 326E 302C 4787  673A 01C4 E7FA AAB2 461C
# uid                  MongoDB 2.6 Release Signing Key <packaging@mongodb.com>
	0C49F3730359A14518585931BC711F9BA15703C6 
# https://docs.mongodb.com/manual/tutorial/verify-mongodb-packages/#download-then-import-the-key-file
RUN set -ex; \
	export GNUPGHOME="$(mktemp -d)"; \
	for key in $GPG_KEYS; do \
		gpg --keyserver ha.pool.sks-keyservers.net --recv-keys "$key"; \
	done; \
	gpg --export $GPG_KEYS > /etc/apt/trusted.gpg.d/mongodb.gpg; \
	apt-key list

ARG MONGO_PACKAGE=mongodb-org
ARG MONGO_REPO=repo.mongodb.org
ENV MONGO_PACKAGE=${MONGO_PACKAGE} MONGO_REPO=${MONGO_REPO}

ENV MONGO_MAJOR 3.4
ENV MONGO_VERSION 3.4.9

RUN echo "deb http://$MONGO_REPO/apt/debian jessie/${MONGO_PACKAGE%-unstable}/$MONGO_MAJOR main" | tee "/etc/apt/sources.list.d/${MONGO_PACKAGE%-unstable}.list"

RUN set -x \
	&& apt-get update \
	&& apt-get install -y \
		${MONGO_PACKAGE}-shell=$MONGO_VERSION \
		${MONGO_PACKAGE}-tools=$MONGO_VERSION \
	&& rm -rf /var/lib/apt/lists/* \

RUN echo "deb http://ftp.utexas.edu/dotdeb/ stable all" >>  /etc/apt/sources.list.d/dotdeb.list

RUN echo "deb-src http://ftp.utexas.edu/dotdeb/ stable all" >>  /etc/apt/sources.list.d/dotdeb.list

RUN wget https://www.dotdeb.org/dotdeb.gpg && apt-key add dotdeb.gpg

RUN set -x \
  && apt update \
  && apt install -y \
  redis-server \
  && rm -rf /var/lib/apt/lists/* \
