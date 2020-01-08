FROM debian:stable

LABEL maintainer="myugan59@gmail.com"
LABEL version="6.4.2"

ENV DEBIAN_FRONTEND=noninteractive
ENV ELASTICSEARCH_IP="localhost"

# Install general package
RUN apt-get update && apt-get -y upgrade
RUN apt-get -y install software-properties-common apt-transport-https sudo git nano curl wget net-tools

# Add elastic repository
RUN echo "deb https://artifacts.elastic.co/packages/6.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-6.x.list
RUN apt-get update

# Install kibana
RUN apt-get -y --allow-unauthenticated install kibana
ADD kibana.yml /etc/kibana/kibana.yml

ADD ./entrypoint.sh /
RUN chmod +x /entrypoint.sh

EXPOSE 5601
ENTRYPOINT [ "/bin/bash" , "/entrypoint.sh"]