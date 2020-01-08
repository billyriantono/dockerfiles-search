FROM openjdk:8

USER root
#oleUN  apt update
RUN  apt-get update && apt-get install -y apt-transport-https
#RUN  sudo apt-get install -y default-jre
RUN  apt-get install -y wget
RUN  wget --no-check-certificate -O - https://debian.neo4j.org/neotechnology.gpg.key | apt-key add -
RUN  echo 'deb http://debian.neo4j.org/repo stable/' | tee /etc/apt/sources.list.d/neo4j.list
RUN  apt-get update
RUN  apt-get install -y neo4j=1:3.4.9

EXPOSE 7474 7473 7687

ENTRYPOINT ["neo4j"]
CMD ["console"]
