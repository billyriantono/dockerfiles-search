FROM node:5
RUN apt-get -y update && apt-get -y install nginx
RUN apt-get -y install moreutils
ADD start.sh /docker-start
ENTRYPOINT ["/docker-start"]
