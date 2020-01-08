FROM cassandra:3
RUN apt-get update && apt-get install -y wget
RUN wget -qO- https://github.com/vogsphar/logback-gelf/archive/v1.1.0-compiled.tar.gz | tar xvz --strip-components=2 -C /usr/share/cassandra/lib logback-gelf-1.1.0-compiled/rel/logback-gelf-1.1.0.jar
