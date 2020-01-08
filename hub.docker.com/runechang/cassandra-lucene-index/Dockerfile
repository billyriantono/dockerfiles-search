FROM openjdk:8u191-jdk-alpine3.9
RUN apk --no-cache add git maven \
  && git clone http://github.com/Stratio/cassandra-lucene-index 
WORKDIR /cassandra-lucene-index
RUN git checkout 3.0.17.0 \
  && mvn clean package

FROM cassandra:3.0.17  
COPY --from=0 /cassandra-lucene-index/plugin/target/cassandra-lucene-index-plugin-*.jar /usr/share/cassandra/lib/
