FROM openjdk:14-slim-buster

RUN apt-get update && apt-get install -y curl jq

LABEL maintainer="Shawak#2625 (maxi.nussbaum@gmail.com)"

ARG tag=latest
ENV TAG=$tag

RUN mkdir /app && \
	cd /app

WORKDIR /app

COPY ./build.sh /build.sh
RUN sed -i 's/\r$//' /build.sh && \
	chmod +x /build.sh && \
	bash -c "/build.sh"

COPY ./docker-entrypoint.sh /docker-entrypoint.sh
RUN sed -i 's/\r$//' /docker-entrypoint.sh && \
	chmod +x /docker-entrypoint.sh

ENTRYPOINT ["/docker-entrypoint.sh"]