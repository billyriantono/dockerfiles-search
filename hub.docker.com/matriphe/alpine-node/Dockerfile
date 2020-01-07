# Use Alpine Linux
FROM alpine:latest

# Declare maintainer
MAINTAINER Muhammad Zamroni <halo@matriphe.com>

# Timezone
ENV TIMEZONE Asia/Jakarta

ENV NODE_VERSION 0.12.2
ENV NPM_VERSION 3.5.0

# Let's roll
RUN	apk update && \
	apk upgrade && \
	apk add --update tzdata && \
	cp /usr/share/zoneinfo/${TIMEZONE} /etc/localtime && \
	echo "${TIMEZONE}" > /etc/timezone && \
	apk add --update nodejs && \
	npm install -g npm@"${NPM_VERSION}" && \
	npm cache clean -f && \
	apk del tzdata && \
	mkdir /www && \
	rm -rf /var/cache/apk/*

# Set Workdir
WORKDIR /www

# Expose volumes
VOLUME ["/www"]

# Entry point
CMD ["node"]