#small apache img to run kibana 
#

FROM httpd:2.4

MAINTAINER b13n1u <b13n1u@gmail.com>

ENV KB_VERSION 3.1.2

RUN apt-get update && apt-get -q -y install wget && apt-get clean

RUN wget -q https://download.elasticsearch.org/kibana/kibana/kibana-$KB_VERSION.tar.gz -O - | tar zxvf - -C /usr/local/apache2/htdocs/ && \
    mv /usr/local/apache2/htdocs/kibana-$KB_VERSION /usr/local/apache2/htdocs/kibana/

	
EXPOSE 80
EXPOSE 443
