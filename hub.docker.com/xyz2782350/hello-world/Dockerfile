#Version: 0.0.1
FROM ubuntu
MAINTAINER xuyongzheng "xyz2782350@163.com"
ENV REFRESHED_AT 2017-05-02
USER root
VOLUME ["/opt/project"]
RUN apt-get update
RUN apt-get install -y nginx
ENTRYPOINT ["/usr/sbin/nginx"]
CMD ["-h"]
RUN echo 'Hi, I am in your container' >/usr/share/nginx/html/index.html
EXPOSE 80
