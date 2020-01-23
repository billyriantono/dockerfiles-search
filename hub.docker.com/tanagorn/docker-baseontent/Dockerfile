FROM nginx
MAINTAINER Ömer Yildiz <hallo@systemfreund.com>

ADD https://download.elasticsearch.org/kibana/kibana/kibana-3.1.0.tar.gz /tmp/
RUN ["mkdir", "-p", "/web/"]
RUN ["tar", "-C", "/web", "-xf", "/tmp/kibana-3.1.0.tar.gz"]
RUN ["cp", "/web/kibana-3.1.0/app/dashboards/logstash.json", "/web/kibana-3.1.0/app/dashboards/default.json"]

COPY nginx.conf /etc/nginx/nginx.conf
COPY config.js /web/kibana-3.1.0/config.js
