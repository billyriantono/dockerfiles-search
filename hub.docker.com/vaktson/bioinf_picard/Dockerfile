FROM ubuntu:19.04
RUN apt-get update && apt-get install -y wget openjdk-8-jdk && wget https://github.com/broadinstitute/picard/releases/download/2.20.2/picard.jar
RUN echo '#!/bin/bash\njava -jar /picard.jar' > /usr/bin/picard && chmod +x /usr/bin/picard
