# A Dockerfile for creating a Kibana container that is designed
# to work with Kubernetes logging.

FROM tutum/nginx
MAINTAINER Bin Zhao <wo@zhaob.in>

RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y wget && \
    rm -rf /var/cache/apt/* && rm -rf /var/lib/apt/lists/*

ENV KIBANA_VERSION 3.1.1

RUN wget http://download.elasticsearch.org/kibana/kibana/kibana-${KIBANA_VERSION}.tar.gz -O kibana.tar.gz && \
    tar xf kibana.tar.gz && \
    mv kibana-${KIBANA_VERSION}/* /usr/share/nginx/html && \
    rm kibana.tar.gz

# ADD default /etc/nginx/sites-available/default
ADD run_kibana_nginx.sh /usr/local/bin/run_kibana_nginx.sh

EXPOSE 80
CMD ["/usr/local/bin/run_kibana_nginx.sh"]
