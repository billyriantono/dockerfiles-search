#
# Build: docker build -t apt-cacher .
# Run: docker run -d -p 3142:3142 --name apt-cacher-run apt-cacher
#
# and then you can run containers with:
#   docker run -t -i --rm -e http_proxy http://dockerhost:3142/ debian bash
#
# Here, `dockerhost` is the IP address or FQDN of a host running the Docker daemon
# which acts as an APT proxy server.
FROM        ubuntu:18.04

RUN     apt-get update \
	&& apt-get install -y apt-cacher-ng curl \
	&& apt-get autoclean \
	&& apt-get autoremove \
	&& mkdir -p /var/cache/apt-cacher-ng/_import \
	&& chown apt-cacher-ng /var/cache/apt-cacher-ng/_import

EXPOSE      3142

CMD     chmod 777 /var/cache/apt-cacher-ng && /etc/init.d/apt-cacher-ng start && tail -f /var/log/apt-cacher-ng/*

VOLUME      ["/var/cache/apt-cacher-ng"]
VOLUME      ["/var/log/apt-cacher-ng"]
VOLUME      ["/etc/apt-cacher-ng"]


HEALTHCHECK --interval=20s --timeout=2s --retries=3 \
    CMD curl -f http://localhost:3142/acng-report.html || exit 1
