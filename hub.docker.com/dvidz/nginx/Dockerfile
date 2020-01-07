FROM debian:jessie

MAINTAINER David Souvignon <david.souvignon@gmail.com>

ARG VIRTUAL_HOST=symfony.dev
ARG FPM_HOST=engine
ARG FPM_PORT=9000

ENV VIRTUAL_HOST ${VIRTUAL_HOST}
ENV FPM_HOST ${FPM_HOST}
ENV FPM_PORT ${FPM_PORT}

RUN apt-get update && apt-get install -y \
    nginx

ADD assets/nginx.conf /etc/nginx/
ADD assets/default-sf3.conf /etc/nginx/sites-available/

RUN ln -s /etc/nginx/sites-available/default-sf3.conf /etc/nginx/sites-enabled/symfony
RUN rm /etc/nginx/sites-enabled/default

RUN usermod -u 1000 www-data

COPY start.sh /usr/local/bin/start.sh
RUN chmod +x usr/local/bin/start.sh

CMD ["start.sh"]

#CMD ["nginx"]
#
EXPOSE 80
EXPOSE 443