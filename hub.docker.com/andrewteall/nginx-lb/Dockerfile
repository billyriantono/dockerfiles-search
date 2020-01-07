
FROM nginx
MAINTAINER Andrew Teall <andrewteall@gmail.com>

ADD default.conf /etc/nginx/nginx.conf

RUN apt-get update && apt-get install -y wget golang git

WORKDIR /opt
RUN git clone git://github.com/elasticsearch/logstash-forwarder.git 

WORKDIR /opt/logstash-forwarder
RUN go build -o logstash-forwarder
RUN find ! -name 'logstash-forwarder' ! -name '.'  -exec rm -rf {} +
ADD logstash-forwarder.conf /opt/logstash-forwarder/logstash-forwarder.conf
RUN ls
RUN touch /var/log/nginx/access_log
RUN chmod 0777 /var/log/nginx/access_log
RUN chmod 0777 /opt/logstash-forwarder/logstash-forwarder
ADD logstash-forwarder.crt /opt/logstash-forwarder/logstash-forwarder.crt
CMD /usr/sbin/nginx -c  /etc/nginx/nginx.conf && echo "199.223.235.196 logstash.example.com" >> /etc/hosts && cat /etc/hosts && /opt/logstash-forwarder/logstash-forwarder -config /opt/logstash-forwarder/logstash-forwarder.conf
