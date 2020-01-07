FROM debian:stretch
RUN set -x \
	&& apt update \
	&& apt upgrade -y \
	&& apt-get install -y redis-server \
	&& apt-get clean -y

COPY docker-entrypoint.sh /usr/local/bin/
RUN ln -s /usr/local/bin/docker-entrypoint.sh /
ENTRYPOINT ["docker-entrypoint.sh"]
EXPOSE 6379
CMD ["redis-server"]
