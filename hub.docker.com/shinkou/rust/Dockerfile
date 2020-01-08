FROM debian:stretch
RUN set -x \
	&& apt update \
	&& apt upgrade -y \
	&& apt-get install -y curl gcc \
	&& apt-get clean -y
RUN curl https://sh.rustup.rs -sSf | sh -s -- -y

COPY docker-entrypoint.sh /usr/local/bin/
RUN ln -s /usr/local/bin/docker-entrypoint.sh /
ENTRYPOINT ["docker-entrypoint.sh"]
WORKDIR /data
CMD ["bash"]
