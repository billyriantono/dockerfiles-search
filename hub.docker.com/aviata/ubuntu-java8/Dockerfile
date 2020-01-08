FROM aviata/ubuntu

# Java SE 8

RUN  date -u +"%Y-%m-%d %H:%M:%S" && echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | debconf-set-selections \
  && date -u +"%Y-%m-%d %H:%M:%S" && add-apt-repository -y ppa:webupd8team/java \
  && date -u +"%Y-%m-%d %H:%M:%S" && apt-get update \
  && date -u +"%Y-%m-%d %H:%M:%S" && apt-get install -y oracle-java8-installer \
  && date -u +"%Y-%m-%d %H:%M:%S" && rm -rf /var/lib/apt/lists/* \
  && date -u +"%Y-%m-%d %H:%M:%S" && rm -rf /var/cache/oracle-jdk8-installer \
  && date -u +"%Y-%m-%d %H:%M:%S"
