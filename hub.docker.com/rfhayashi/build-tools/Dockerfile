FROM openjdk:7u111-jdk

MAINTAINER Rui Fernando Hayashi <rfhayashi@gmail.com>

# rake
RUN apt-get update && apt-get install -y rake=10.3.2-2

# leiningen
ENV LEIN_ROOT true
RUN wget -q -O /usr/bin/lein \
        https://raw.githubusercontent.com/technomancy/leiningen/stable/bin/lein \
        && chmod +x /usr/bin/lein && lein upgrade 2.6.1

# app engine sdk
RUN wget -q -O /usr/local/appengine-java-sdk-1.9.42.zip https://storage.googleapis.com/appengine-sdks/featured/appengine-java-sdk-1.9.42.zip \
    && unzip /usr/local/appengine-java-sdk-1.9.42.zip -d /usr/local && rm /usr/local/appengine-java-sdk-1.9.42.zip
ENV PATH $PATH:/usr/local/appengine-java-sdk-1.9.42/bin