FROM felixkazuyadev/base-image
MAINTAINER Felix Kazuya <me@felixkazuya.de>
MAINTAINER Christian Walonka <cwalonka@it-economics.de>
ENV REFRESHED_AT 2019-03-04


RUN echo debconf shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && add-apt-repository ppa:webupd8team/java && apt-get update && apt-get install -y oracle-java8-installer && apt-get clean && apt-get autoclean && apt-get autoremove && rm -rf /var/cache/oracle-jdk*
