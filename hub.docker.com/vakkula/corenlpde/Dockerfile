FROM java:jre-alpine

MAINTAINER vk <vakkula@gmail.com>

RUN apk add --update --no-cache \
	 wget

RUN wget -P /opt/corenlp/ http://nlp.stanford.edu/software/stanford-german-corenlp-2018-10-05-models.jar

RUN export CLASSPATH="`find . -name '*.jar'`"

ENV PORT 9000

EXPOSE $PORT

CMD java -cp "/opt/corenlp/" -mx4g edu.stanford.nlp.pipeline.StanfordCoreNLPServer