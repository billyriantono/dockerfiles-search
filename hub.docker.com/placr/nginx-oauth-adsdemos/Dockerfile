# Do not use this docker in a production environment, just for demo purposes.

FROM        debian:jessie
MAINTAINER  Jan Verhoeven <jan@visity.nl>

RUN         apt-get update && \
            apt-get install -y nginx nginx-extras lua-json lua-sec && \
            rm -rf /var/lib/apt/lists/*

RUN         rm /etc/nginx/sites-enabled/default
ADD         nginx/demo.conf /etc/nginx/sites-enabled/
ADD         nginx/access.lua /etc/nginx/nginx-google-oauth/access.lua

# Add certificates for HTTPS
RUN			mkdir -p /etc/nginx/certs/
ADD			nginx/*.crt /etc/nginx/certs/
ADD			nginx/*.key /etc/nginx/certs/

# forward request and error logs to docker log collector
RUN         ln -sf /dev/stdout /var/log/nginx/access.log
RUN         ln -sf /dev/stderr /var/log/nginx/error.log

COPY        docker-entrypoint.sh /

ENTRYPOINT ["/docker-entrypoint.sh"]

EXPOSE      443

CMD 		["nginx", "-g", "daemon off;"]