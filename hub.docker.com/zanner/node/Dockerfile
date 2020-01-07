FROM progrium/busybox:latest

MAINTAINER Sergyi Kukharyev <sergej.kucharev@gmail.com>

ARG user=node
ARG group=${user}
RUN adduser -s /bin/false -D ${user} ${group}

RUN opkg-install opkg && opkg update
RUN opkg install vim
RUN opkg install htop
#RUN opkg install git
RUN opkg install node
RUN npm install -g supervisor
RUN npm install -g http

COPY data /data
RUN chmod -R a+r,u+w,g+w /data

RUN mkdir -pv -m a+r,a+x,u+w /docker
COPY docker/*.sh /docker/
RUN chmod -R +x /docker/*.sh

ENTRYPOINT ["/docker/enterpoint.sh"]
EXPOSE 80
