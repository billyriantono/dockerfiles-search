FROM centos
MAINTAINER tangchen tangchen2018@hotmail.com

COPY install /root
COPY web /root
RUN sh /root/install.sh

RUN rm -rf /usr/local/nginx/conf/nginx.conf /usr/local/nginx/conf/conf.d
COPY ./nginx.conf /usr/local/nginx/conf/
COPY ./vhost /usr/local/nginx/conf/vhost

CMD ["/usr/local/nginx/sbin/nginx", "-g", "daemon off;"]
