FROM debian:stretch

RUN dpkg --add-architecture i386 \
		&& apt-get update && apt-get install -y wget gnupg2 \
        && wget https://dl.winehq.org/wine-builds/Release.key \
		&& apt-key add Release.key \
        && apt-get install -y apt-transport-https \
        && echo "deb https://dl.winehq.org/wine-builds/debian/ stretch main" >> /etc/apt/sources.list \
		&& apt-get update && apt-get install -y --no-install-recommends \
			winehq-stable \
		&& rm -rf /var/lib/apt/lists/*


