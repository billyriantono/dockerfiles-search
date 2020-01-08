FROM kalamangga/java-openjdk:8
RUN apt update && \
  apt install -y gnupg2 && \
  curl -v http://public-repo-1.hortonworks.com/ambari/debian9/2.x/updates/2.7.1.0/ambari.list \
  -o /etc/apt/sources.list.d/ambari.list && \
  apt-key adv --recv-keys --keyserver keyserver.ubuntu.com B9733A7A07513CAD && \
  apt update && \
  apt install -y ambari-server && \
  ambari-server setup --silent --java-home /usr/lib/jvm/java-8-openjdk-amd64
COPY init.sh /
EXPOSE 8080
CMD ["/init.sh"]
