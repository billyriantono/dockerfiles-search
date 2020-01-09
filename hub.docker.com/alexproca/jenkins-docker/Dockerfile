FROM jenkins

USER root

RUN apt-get update
RUN apt-get install apt-transport-https ca-certificates -y
RUN apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
RUN echo "deb https://apt.dockerproject.org/repo debian-jessie main" > /etc/apt/sources.list.d/docker.list
RUN apt-get update
RUN apt-get install docker-engine -y
RUN curl -sL https://deb.nodesource.com/setup_7.x | bash -
RUN apt-get install nodejs -y
RUN npm install -g yarn

ADD start.sh /start.sh

ENTRYPOINT ["/bin/tini", "--", "/start.sh"]