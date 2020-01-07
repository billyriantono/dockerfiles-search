FROM eeacms/apache:2.4s
MAINTAINER "EEA: IDM2 C-TEAM" <eea-edw-c-team-alerts@googlegroups.com>

ENV SERVER_ADMIN="root@localhost"
ENV SERVER_NAME="localhost"

ADD apache.conf /usr/local/apache2/conf/extra/vh-my-app.conf
ADD custom_50x.html /usr/local/apache2/htdocs/custom_50x.html
