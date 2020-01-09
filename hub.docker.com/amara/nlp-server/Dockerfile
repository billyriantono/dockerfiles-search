FROM alpine:3.8
MAINTAINER Ben Dean-Kawamura <ben@pculture.org>

RUN apk update && apk add curl openjdk8-jre-base

# install latest CoreNLP release
WORKDIR /opt
RUN curl -OL http://nlp.stanford.edu/software/stanford-corenlp-full-2018-10-05.zip && \
    unzip stanford-corenlp-full-*.zip && \
    mv $(ls -d stanford-corenlp-full-*/) corenlp && \
    rm *.zip

# install latest English language model
#
WORKDIR /opt/corenlp
RUN curl -OL http://nlp.stanford.edu/software/stanford-english-corenlp-2018-10-05-models.jar

COPY server.properties /opt/corenlp

ENV MAX_MEMORY 4g
EXPOSE 9000
CMD java -Xmx$MAX_MEMORY -cp "*" edu.stanford.nlp.pipeline.StanfordCoreNLPServer -props server.properties -port 9000 -timeout 15000
