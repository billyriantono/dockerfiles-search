FROM debian:stretch
LABEL maintainer="Sergey Cherepanov <s@cherepanov.co>"
LABEL name="djocker/debian"
ARG DEBIAN_FRONTEND=noninteractive
ENV LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8 LANGUAGE=en_US.UTF-8
RUN apt-get update \
	&& apt-get install -y --no-install-recommends locales \
	&& apt-get clean \
	&& rm -rf /var/lib/apt/lists/* \
	&& sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen \
	&& dpkg-reconfigure locales \
	&& update-locale LANG=en_US.UTF-8