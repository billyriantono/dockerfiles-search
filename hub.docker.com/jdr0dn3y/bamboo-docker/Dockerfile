# Basics
#
FROM jdr0dn3y/dev-studio-base
MAINTAINER Justin Donnaruma <justin@rumatec.us>

# Install bamboo

ENV BAMBOO_VERSION 5.6.1
RUN curl -Lks http://www.atlassian.com/software/bamboo/downloads/binary/atlassian-bamboo-${BAMBOO_VERSION}.tar.gz -o /root/bamboo.tar.gz
RUN /usr/sbin/useradd --create-home --home-dir /home/bamboo --shell /bin/bash bamboo
RUN mkdir /opt/bamboo
RUN tar zxf /root/bamboo.tar.gz --strip=1 -C /opt/bamboo
RUN echo "bamboo.home= /home/bamboo" > /opt/bamboo/atlassian-bamboo/WEB-INF/classes/bamboo-init.properties
RUN chown -R bamboo:bamboo /opt/bamboo

RUN mkdir /etc/service/bamboo
ADD bamboo.sh /etc/service/bamboo/run

RUN chmod +x /etc/service/bamboo/run
RUN chown root: /etc/service/bamboo/run
# Launching bamboo

EXPOSE 8085
