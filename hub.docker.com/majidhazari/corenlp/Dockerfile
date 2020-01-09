FROM java:jre-alpine

MAINTAINER Majid Hazari <majid.hazari@gmail.com>

RUN apk add --update --no-cache \
	 unzip \
	 wget

RUN wget --no-verbose http://nlp.stanford.edu/software/stanford-corenlp-full-2018-10-05.zip && \
	unzip stanford-corenlp-full-2018-10-05.zip && \
	wget --no-verbose -P stanford-corenlp-full-2018-10-05/ http://nlp.stanford.edu/software/stanford-arabic-corenlp-2018-10-05-models.jar && \
	wget --no-verbose -P stanford-corenlp-full-2018-10-05/ http://nlp.stanford.edu/software/stanford-chinese-corenlp-2018-10-05-models.jar && \
	wget --no-verbose -P stanford-corenlp-full-2018-10-05/ http://nlp.stanford.edu/software/stanford-english-corenlp-2018-10-05-models.jar && \
	wget --no-verbose -P stanford-corenlp-full-2018-10-05/ http://nlp.stanford.edu/software/stanford-english-kbp-corenlp-2018-10-05-models.jar && \
	wget --no-verbose -P stanford-corenlp-full-2018-10-05/ http://nlp.stanford.edu/software/stanford-french-corenlp-2018-10-05-models.jar && \
	wget --no-verbose -P stanford-corenlp-full-2018-10-05/ http://nlp.stanford.edu/software/stanford-german-corenlp-2018-10-05-models.jar && \
	wget --no-verbose -P stanford-corenlp-full-2018-10-05/ http://nlp.stanford.edu/software/stanford-spanish-corenlp-2018-10-05-models.jar && \
	rm *.zip

WORKDIR stanford-corenlp-full-2018-10-05

RUN export CLASSPATH="`find . -name '*.jar'`"

ENV PORT 9000

EXPOSE $PORT

CMD java -cp "*" -mx8g edu.stanford.nlp.pipeline.StanfordCoreNLPServer
