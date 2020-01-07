FROM nginx:1.17.1-alpine

RUN apk add --no-cache --update python3 ca-certificates bash wget openssl \
	&& pip3 install --upgrade pip \
	&& update-ca-certificates \
	&& pip3 install docker \ 
	&& echo 'daemon off;' >> /etc/nginx/nginx.conf

WORKDIR /app

COPY ./app .

ENV DOCKER_HOST unix:///tmp/docker.sock

VOLUME ["/etc/nginx/certs", "/etc/nginx/dhparam", "/tmp/docker.sock"]

ENTRYPOINT ["/usr/bin/env"]

CMD ["/usr/bin/python3", "/app/main.py"]

EXPOSE 80 443

