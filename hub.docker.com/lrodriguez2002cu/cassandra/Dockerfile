FROM cassandra:3.11

ENV JACKSON_VERSION 1.9.13
ENV OLD_JACKSON_VERSION 1.9.2

ENV old_core_lib jackson-core-asl-${OLD_JACKSON_VERSION}.jar
ENV old_mapper_lib jackson-mapper-asl-${OLD_JACKSON_VERSION}.jar

#new names  of the jackson libs
ENV core_lib  jackson-core-asl-${JACKSON_VERSION}.jar
ENV mapper_lib jackson-mapper-asl-${JACKSON_VERSION}.jar

ENV core_lib_url   http://central.maven.org/maven2/org/codehaus/jackson/jackson-core-asl/${JACKSON_VERSION}/jackson-core-asl-${JACKSON_VERSION}.jar
ENV mapper_lib_url http://central.maven.org/maven2/org/codehaus/jackson/jackson-mapper-asl/${JACKSON_VERSION}/jackson-mapper-asl-${JACKSON_VERSION}.jar

#install the wget
RUN apt-get update && apt-get install -y --no-install-recommends ca-certificates wget

RUN rm /usr/share/cassandra/lib/${old_core_lib} && rm /usr/share/cassandra/lib/${old_mapper_lib}

RUN wget -O /usr/share/cassandra/lib/${core_lib}  ${core_lib_url} && wget -O /usr/share/cassandra/lib/${mapper_lib}  ${mapper_lib_url}