# version: 0.0.2
FROM ubuntu:14.04
MAINTAINER xueren "281125249@163.com"
RUN apt-get update
RUN apt-get install -y nginx                    
ENV REFRESHED_AT 2018-07-13
ADD ./web_html/ /usr/share/nginx/html/
EXPOSE 80   
ENTRYPOINT ["/usr/sbin/nginx"]
CMD ["-g","daemon off;"]
