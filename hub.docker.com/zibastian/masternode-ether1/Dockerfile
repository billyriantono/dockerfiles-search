FROM ubuntu:16.04
MAINTAINER Zibastian <Discord: @zibastian>

RUN apt-get update \
	&& apt-get install -y --no-install-recommends wget ca-certificates \
	&& rm -rf /var/lib/apt/lists/*

ARG usr=etho
RUN groupadd -g 900 ${usr} && \
    useradd -r -u 900 -g ${usr} -d /opt/${usr} ${usr} \
	&& mkdir -p /opt/${usr} \
	&& chown -R ${usr}:${usr} /opt/${usr}

RUN cd /usr/bin/ \
	&& wget -O - https://ether1.org/releases/Ether1-MN-SN-0.0.8.tar.gz | tar xfvz -

COPY ./docker-entrypoint.sh /usr/bin/docker-entrypoint
RUN chmod +x /usr/bin/docker-entrypoint

CMD ["docker-entrypoint"]

USER ${usr}

WORKDIR /opt/${usr}

EXPOSE 30305
EXPOSE 80
EXPOSE 4001
EXPOSE 5001
