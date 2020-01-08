# SOLR EMBEDDED
FROM openjdk:8-jdk

ENV TZ=Europe/Paris

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && \
  echo $TZ > /etc/timezone && \
  apt-get update && \
  apt-get install -y lsof && \
  wget https://github.com/glowroot/glowroot/releases/download/v0.13.5/glowroot-0.13.5-dist.zip -O /tmp/glowroot.zip && \
  unzip /tmp/glowroot.zip  -d / && \
  rm -rf /tmp/glowroot.zip && \
  apt-get clean
  
 EXPOSE 4000
