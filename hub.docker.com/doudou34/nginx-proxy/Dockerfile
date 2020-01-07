 FROM nginx

LABEL MAINTAINER="Edouard COMTET<edouard.comtet@gmail.com>"
LABEL version="1.0"

COPY ./default.conf /etc/nginx/conf.d/default.conf.template
COPY ./start.sh /opt/start.sh

EXPOSE 80

CMD '/opt/start.sh'
