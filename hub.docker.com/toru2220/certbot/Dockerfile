FROM	debian:stretch-slim
eNV     DEBIAN_FRONTEND noninteractive


RUN	apt-get update && \
        apt-get install -y --no-install-recommends certbot && \
	rm -rf /var/lib/apt/lists/*

VOLUME	/etc/letsencrypt/
VOLUME	/data


