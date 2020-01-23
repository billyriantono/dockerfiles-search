FROM ubuntu:trusty
MAINTAINER fblgit@git
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && apt-get upgrade -y && apt-get dist-upgrade -y
RUN apt-get install -qy nginx-full rsync wget && apt-get clean
VOLUME /data
ADD /scripts/ /data/
RUN chmod +x /data/*.sh
EXPOSE 80
EXPOSE 443
RUN /data/install.sh

CMD ["/data/start.sh"]
