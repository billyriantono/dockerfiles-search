FROM debian:stretch-slim

RUN dpkg --add-architecture i386 \
	&& apt-get update \
	&& apt-get install -y --no-install-recommends \
		wine32 \
		wine \
	&& rm -rf /var/lib/apt/lists/*

WORKDIR /app

COPY app/ /app

RUN chmod +x start.sh
# Prefix commands passed into bash so that they run in xvfb

CMD [ "/app/start.sh" ]