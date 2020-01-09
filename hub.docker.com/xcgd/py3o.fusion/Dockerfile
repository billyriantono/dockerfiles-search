# A docker file containing the py3o.fusion server
# it is configured to be linked with a py3o.renderserver docker
FROM ubuntu:18.04
LABEL maintainer="florent.aide@gmail.com"
ARG REVISION=""
ARG CREATED=""
LABEL org.opencontainers.image.revision=$REVISION
LABEL org.opencontainers.image.vendor="XCG"
LABEL org.opencontainers.image.version="0.8.9-3"
LABEL org.opencontainers.image.authors="XCG"
LABEL org.opencontainers.image.created=$CREATED
LABEL org.opencontainers.image.title="py3o.fusion"
#LABEL org.opencontainers.image.description=""

ENV DEBIAN_FRONTEND noninteractive

ADD files /
RUN set -x ; \
	apt-get update \
	&& apt-get -y -q install \
		locales \
		python-setuptools python-pip libxml2 \
		language-pack-fr language-pack-en language-pack-ru language-pack-it language-pack-de \
		language-pack-es language-pack-pt \
	&& apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
RUN pip install --upgrade --use-wheel --no-index --find-links=https://wheelhouse.xcg.io/18.04/py3o.fusion/ -r /usr/src/pip_reqs.txt --system

EXPOSE 8765

CMD ["start-py3o-fusion", "--renderserver=py3orenderserver"]
