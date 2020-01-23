FROM 			ubuntu:14.04
MAINTAINER 		Allan Lei <allanlei@helveticode.com>

RUN 			adduser --disabled-password --gecos "" git
RUN 			apt-get update && apt-get install -y git && apt-get autoremove -y && apt-get autoclean -y

RUN 			mkdir -p /etc/gogs
ADD 			gogs /etc/gogs

EXPOSE 			3000
CMD 			["/etc/gogs/start.sh"]