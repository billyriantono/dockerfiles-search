FROM x110dc/base
MAINTAINER Daniel Craigmile

RUN apt-get update
# apache2-utils only needed for htpasswd command
RUN apt-get install -yq apache2-utils nginx

ADD http://download.elasticsearch.org/kibana/kibana/kibana-latest.tar.gz /tmp/
RUN cd /tmp; tar -zxvf kibana-latest.tar.gz
RUN mv /tmp/kibana-latest /usr/share/nginx/kibana
RUN echo "daemon off;" >> /etc/nginx/nginx.conf
ADD config.js /usr/share/nginx/
ADD kibana-nginx.conf /etc/nginx/conf.d/
RUN rm /etc/nginx/sites-enabled/default
ADD run.sh /run.sh

CMD /run.sh

EXPOSE 80
