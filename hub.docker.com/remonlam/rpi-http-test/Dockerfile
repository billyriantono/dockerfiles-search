FROM remonlam/rpi-rasbian:jessie
MAINTAINER Remon Lam <remon.lam@virtualclouds.info>

RUN apt-get update && apt-get install -y lighttpd wget
RUN rm -rf /var/www/html/index*
RUN wget -P /var/www/html https://raw.githubusercontent.com/remonlam/rpi-http-test/master/cloud_PNG6.png
RUN wget -P /var/www/html https://raw.githubusercontent.com/remonlam/rpi-http-test/master/index.html
RUN wget -P / https://raw.githubusercontent.com/remonlam/rpi-http-test/master/entrypoint.sh
RUN chmod 755 /./entrypoint.sh

CMD /./entrypoint.sh

EXPOSE 80
