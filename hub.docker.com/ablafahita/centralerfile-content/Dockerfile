# Added keeping in min the layers

FROM python:3.7.1-stretch
COPY ./docker-entrypoint.sh /
CMD "apt-get -y update && apt-get -y install iputils-ping net-tools avahi-daemon avahi-utils"
RUN chmod +x docker-entrypoint.sh
ENTRYPOINT ["/docker-entrypoint.sh"]

