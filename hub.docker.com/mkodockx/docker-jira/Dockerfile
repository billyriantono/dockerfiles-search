FROM phusion/baseimage:0.9.17
MAINTAINER  Markus Kosmal <code@m-ko-x.de>

ENV JIRA_VERSION 6.4.8

# prepare dependencies
RUN apt-get update -qq && \
    apt-get install -qqy software-properties-common python-software-properties nano && \
    apt-add-repository ppa:webupd8team/java -y && \
    apt-get update -qq && \
    echo oracle-java7-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections && \
    apt-get install -yqq oracle-java7-installer && \
    apt-get clean -yqq && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# prepare user
RUN useradd --create-home --home-dir /usr/local/jira --shell /bin/bash jira

# prepare fs
RUN mkdir -p /opt/jira /opt/jira-home /etc/my_init.d

# install
WORKDIR /opt/jira
RUN curl -LSs http://downloads.atlassian.com/software/jira/downloads/atlassian-jira-${JIRA_VERSION}.tar.gz -o jira-archive && \
    tar zxf jira-archive --strip=1 && \
    rm -f jira-archive && \
    echo "jira.home = /opt/jira-home" > /opt/jira/atlassian-jira/WEB-INF/classes/jira-application.properties

# Launching Jira
# And add start script in my_init.d of Phusion baseimage
WORKDIR /opt/jira-home
COPY ./start-jira.sh /etc/my_init.d/start-jira.sh

EXPOSE 8080

CMD  ["/sbin/my_init"]
