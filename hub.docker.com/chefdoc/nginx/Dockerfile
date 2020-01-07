FROM nginx:alpine
MAINTAINER Jörg Herzinger <joerg.herzinger+chefdoc@oiml.at>

ADD nginx.conf.template /etc/nginx/nginx.conf.template
ADD run.sh /run-nginx.sh
RUN chmod +x /run-nginx.sh

EXPOSE 80
ENV BACKENDS=""

CMD /run-nginx.sh
