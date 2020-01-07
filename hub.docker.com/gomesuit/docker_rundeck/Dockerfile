FROM java:7

# set timezone
RUN cp -f /usr/share/zoneinfo/Asia/Tokyo /etc/localtime

ADD ./config /rundeck
ADD http://dl.bintray.com/rundeck/rundeck-maven/rundeck-launcher-2.6.7.jar /rundeck
RUN mkdir /rundeck/var

WORKDIR /rundeck

ENV RDECK_BASE /rundeck

EXPOSE 4440

CMD server/sbin/rundeckd start && tail -f server/logs/rundeck.access.log

