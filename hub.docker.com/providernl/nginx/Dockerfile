FROM ubuntu:16.04

MAINTAINER Savvii DevOps "devops@savvii.nl"

RUN apt-get update && apt-get install -y \
  nginx \
  nginx-extras

EXPOSE 80 443

CMD ["nginx", "-g", "daemon off;"]