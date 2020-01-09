FROM ruby:2.6-alpine
LABEL maintainer="akahana-1<akahana@akahana.jp>"

RUN set -x \
	&& apk add --virtual .build-deps --no-cache \
		g++ \
	&& apk add --no-cache make \
	&& gem install asciidoctor-pdf --pre \
	&& gem install asciidoctor-latex --pre \
	&& gem install asciidoctor-pdf-cjk asciidoctor-bibliography \
	&& apk del .build-deps

WORKDIR /root

CMD [ "/bin/ash" ]
