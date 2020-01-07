FROM philippwaller/debian:latest

LABEL org.label-schema.schema-version="1.0" \
	  org.label-schema.name="NodeJS" \
	  org.label-schema.description="NodeJS"

RUN DEBIAN_FRONTEND=noninteractive \
 && echo 'deb https://deb.nodesource.com/node_8.x stretch main' > /etc/apt/sources.list.d/nodesource.list \
 && echo 'deb-src https://deb.nodesource.com/node_8.x stretch main' >> /etc/apt/sources.list.d/nodesource.list \
 && apt-key adv --fetch-keys https://deb.nodesource.com/gpgkey/nodesource.gpg.key \
 && apt-get update \
 && apt-get install -y --no-install-recommends nodejs \
 && rm -rf /var/lib/apt/lists/* /tmp/*

CMD /bin/bash





