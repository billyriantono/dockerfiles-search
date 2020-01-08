FROM nginx:1.7

MAINTAINER F4 <dev@f4-group.com>

ADD https://download.elasticsearch.org/kibana/kibana/kibana-3.1.3.tar.gz /tmp/kibana.tar.gz
ADD run.sh /usr/local/bin/run

RUN tar xzf /tmp/kibana.tar.gz && mv kibana-3.1.3/* /usr/share/nginx/html

EXPOSE 80

CMD ["/usr/local/bin/run"]
