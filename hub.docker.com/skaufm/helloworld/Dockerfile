#
#
FROM ubuntu:14.04
MAINTAINER Docker Newbie

RUN apt-get update
#RUN apt-get upgrade
RUN apt-get install -y nginx
RUN echo "Hello World on nginx greets from ams(01) to m.k. from u. in the south of the world ;) " \
        > /usr/share/nginx/html/index.html


CMD ["nginx", "-g", "daemon off;"]

expose 80

