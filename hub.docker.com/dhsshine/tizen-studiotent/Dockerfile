FROM docker:stable

RUN apk add --no-cache python py2-pip git && \
	pip install docker-compose

ENTRYPOINT ["docker-entrypoint.sh"]