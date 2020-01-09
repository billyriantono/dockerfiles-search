FROM java:8-jre-alpine
MAINTAINER Vishwa <hello@vishwa.be>

# Env's
ENV CORENLP_URL http://nlp.stanford.edu/software/stanford-corenlp-full-2016-10-31.zip

RUN apk add --update --no-cache \
    vim \
    unzip \
    wget

RUN wget ${CORENLP_URL} -O stanford-corenlp.zip
RUN unzip -q stanford-corenlp.zip && \
    rm stanford-corenlp.zip
RUN mv $(find -type d -name 'stanford*') stanford-corenlp

RUN export CLASSPATH="`find /stanford-corenlp -type f -name '*.jar'`"

WORKDIR stanford-corenlp
EXPOSE 9000

CMD java -mx4g -cp "*" edu.stanford.nlp.pipeline.StanfordCoreNLPServer -port 9000 -timeout 30000
