FROM mhart/alpine-node:6

RUN apk update \
	&& apk add git

# https://github.com/docker/docker/issues/25925
COPY start.sh /usr/src/start.sh

EXPOSE 3000

CMD [ "/usr/src/start.sh" ]
