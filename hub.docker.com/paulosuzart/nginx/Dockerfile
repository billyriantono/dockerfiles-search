FROM jwilder/nginx-proxy
MAINTAINER Paulo Suzart paulosuzart@gmail.com

RUN rm -f /usr/local/bin/docker-gen

RUN wget https://github.com/jwilder/docker-gen/releases/download/0.3.4/docker-gen-linux-amd64-0.3.4.tar.gz
RUN tar -C /usr/local/bin -xvzf docker-gen-linux-amd64-0.3.4.tar.gz

WORKDIR /app

ADD nginx.tmpl /app/nginx.tmpl
CMD ["forego", "start", "-r"]



