FROM openjdk:8-alpine

LABEL maintainer="Hidekazu Takatsuji<akahana@akahana.jp>"
ENV REDPEN_VER="1.10.1"
ENV PATH="/usr/local/redpen/bin:${PATH}"

RUN set -x \
	&& cd tmp \
	&& wget "https://github.com/redpen-cc/redpen/releases/download/redpen-${REDPEN_VER}/redpen-${REDPEN_VER}.tar.gz" \
	&& tar xf redpen-${REDPEN_VER}.tar.gz \
	&& mv redpen-*/ /usr/local/redpen \
	&& rm redpen-${REDPEN_VER}.tar.gz

CMD ["/bin/sh"]
