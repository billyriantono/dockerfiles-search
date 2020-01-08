
FROM f69m/ubuntu32:stable

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get -y update && \
	apt-get -y install --no-install-recommends runit && \
	apt-get clean && rm -rf /tmp/* /var/tmp/* /var/lib/apt/lists/*

COPY config/runit /etc/runit

CMD ["/sbin/runit"]

