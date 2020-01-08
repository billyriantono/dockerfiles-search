FROM debian:wheezy

RUN apt-get update
RUN apt-get upgrade -f
RUN apt-get -y install openjdk-7-jre-headless -V
RUN apt-get -y install -f

ENV DEBIAN_FRONTEND noninteractive
RUN apt-get purge locales && \
apt-get install -y aptitude && \
aptitude update && \
aptitude install locales && \
echo -e 'LANG="en_US.UTF-8"\nLANGUAGE="en_US:en"\n' > /etc/default/locale && \
aptitude upgrade

RUN locale-gen en_US.UTF-8
RUN echo -e 'LANG="en_US.UTF-8"\nLANGUAGE="en_US:en"\n' > /etc/default/locale

RUN apt-get -y install wget && \
apt-get upgrade && \
echo "deb http://packages.unifiedviews.eu/debian/ wheezy main" > /etc/apt/sources.list.d/unifiedviews.list && \
wget -O - http://packages.unifiedviews.eu/key/unifiedviews.gpg.key | apt-key add - && \
apt-get update && \
apt-get install -y aptitude && \
aptitude update && \
aptitude upgrade

RUN aptitude install -y unifiedviews-mysql
RUN aptitude install -y unifiedviews-pgsql
RUN aptitude install -y unifiedviews-plugins





VOLUME /data
CMD service unifiedviews-backend  start
CMD echo $JAVA_HOME