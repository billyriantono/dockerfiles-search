FROM java:jre-alpine

MAINTAINER Andrew G. <ag@agi.net.ua>

RUN apk add --update --no-cache \
	 unzip \
	 wget
         
RUN wget http://nlp.stanford.edu/software/stanford-corenlp-full-2018-10-05.zip
RUN wget http://nlp.stanford.edu/software/stanford-german-corenlp-2018-10-05-models.jar

RUN unzip stanford-corenlp-full-2018-10-05.zip
RUN rm stanford-corenlp-full-2018-10-05.zip
RUN mv stanford-german-corenlp-2018-10-05-models.jar stanford-corenlp-full-2018-10-05

WORKDIR stanford-corenlp-full-2018-10-05 

RUN export CLASSPATH="`find . -name '*.jar'`"

ENV PORT 9000

EXPOSE $PORT

CMD java -cp "*" -mx8g edu.stanford.nlp.pipeline.StanfordCoreNLPServer -timeout 30000
