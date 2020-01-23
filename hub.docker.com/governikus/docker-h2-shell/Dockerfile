FROM governikus/eidas-base-container:1.0.6
MAINTAINER Benny Prange <benny.prange@governikus.de>

RUN wget http://repo2.maven.org/maven2/com/h2database/h2/1.4.197/h2-1.4.197.jar

ENTRYPOINT ["java", "-cp", "./h2-1.4.197.jar", "org.h2.tools.Shell"]
