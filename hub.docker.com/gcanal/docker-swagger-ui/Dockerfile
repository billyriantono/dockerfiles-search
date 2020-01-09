FROM mhart/alpine-node
MAINTAINER Guillem CANAL "hello@guillem.ninja"

ENV VERSION "2.2.0-alpha"
ENV FOLDER "swagger-ui-$VERSION"
ENV SWAGGER_FILE "/app/swagger.json"

WORKDIR /app

RUN apk update && apk add openssl bash \
	&& wget -qO- https://github.com/guillemcanal/swagger-ui/archive/v$VERSION.tar.gz | tar xvz \
	&& cp -r swagger-ui-$VERSION/dist/* . \
	&& rm -rf swagger-ui-$VERSION \
	&& npm install -g http-server \
	&& apk del openssl

ADD run.sh run.sh

# webserver port
EXPOSE 80

CMD ["sh", "run.sh"]