FROM java

ADD . /cassandra
RUN ls -l /cassandra
RUN  apt-get install openjdk-8-jre
RUN java -version
RUN echo "deb http://debian.datastax.com/community stable main" |  tee -a /etc/apt/sources.list.d/cassandra.sources.list
RUN curl -L http://debian.datastax.com/debian/repo_key |  apt-key add -

RUN  apt-get update
RUN  apt-get -y install dsc20=2.0.11-1 cassandra=2.0.11
